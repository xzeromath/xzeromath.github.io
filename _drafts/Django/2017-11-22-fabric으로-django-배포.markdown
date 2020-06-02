---
# layout: "post"
title: "Fabric으로 django 배포"
date: "2017-11-22 22:14"
# categories: Django
slug: deploy_fabric
tag: Django
header:
  teaser: /assets/images/11.png

---

## 장고 배포 방법

1. manage.py에 있는 곳에 fabfile.py 를 아래와 같이 만든다.
2. 같은 위치에 deploy.json 과 envs.json (빈파일)을 만든다.


{% highlight python %}
# fabfile.py
from fabric.contrib.files import append, exists, sed, put
from fabric.api import env, local, run, sudo
import random
import os
import json

PROJECT_DIR = os.path.dirname(os.path.abspath(__file__))#settings 가 있는 제일 상위 폴더
# PROJECT_DIR = os.path.join(os.path.dirname(os.path.abspath(__file__)),'fbtest')
# PROJECT_DIR = './fbtest' # settings가 있는 폴더

with open(os.path.join(PROJECT_DIR, "deploy.json")) as f:
    envs = json.loads(f.read())

def get_env(setting, envs):
    return envs[setting]

# TODO: Required Fields: REPO_URL, PROJECT_NAME, REMOTE_HOST, REMOTE_PASSWORD, REMOTE_USER @ deploy.json

# developer: chagne this!
REPO_URL = get_env('REPO_URL', envs)
PROJECT_NAME = get_env('PROJECT_NAME', envs)
REMOTE_HOST = get_env('REMOTE_HOST', envs)
REMOTE_HOST_SSH = get_env('REMOTE_HOST_SSH', envs)
REMOTE_USER = get_env('REMOTE_USER', envs)
REMOTE_PASSWORD = get_env('REMOTE_PASSWORD', envs)
STATIC_ROOT_NAME = 'static'   #---------------------------- 수정
STATIC_URL_NAME = 'static'    #---------------------------- 수정
MEDIA_ROOT = 'media'          #---------------------------- 수정

# TODO: Server Engineer: you should add env.user as sudo user and NOT be root
env.user = REMOTE_USER
username = REMOTE_USER
# Option: env.password
env.hosts = [
    REMOTE_HOST_SSH,
]
env.password = REMOTE_PASSWORD
project_folder = '/home/{}/{}'.format(env.user, PROJECT_NAME)
apt_requirements = [
    'curl',
    'git',
    'python3-dev',
    'python3-pip',
    'build-essential',
    'libpq-dev',
    'postgresql',
    'postgresql-contrib',
    'apache2',
    'libapache2-mod-wsgi-py3',
    'python3-setuptools',
    'libssl-dev',
    'libffi-dev',
]

def new_server():
    setup()
    deploy()

def setup():
    _mkdir_ssh()
    _register_ssh_key()
    _get_latest_apt()
    _install_apt_requirements(apt_requirements)
    _make_virtualenv()
    #_ufw_allow()

def deploy():
    _get_latest_source()
    _put_envs()
    _update_settings()
    _update_virtualenv()
    _update_static_files()
    _update_database()
    #_ufw_allow()
    _make_virtualhost()
    _grant_apache2()
    _restart_apache2()


def create_superuser():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    run('cd %s && %s/bin/python3 manage.py createsuperuser' % (
        project_folder, virtualenv_folder
    ))

def myg(val="blank"):
    '''git push하고 배포'''
    local('git add .')
    local('git commit -m {}'.format(val))
    local('git push')
    deploy()


def _mkdir_ssh():
    USER_HOME = os.path.expanduser('~')
    if not os.path.exists(os.path.join(USER_HOME, '.ssh/')):
        local("mkdir {}".format(os.path.join(USER_HOME, '.ssh')))

def _register_ssh_key():
    local("ssh-keyscan -H {} >> {}".format(REMOTE_HOST, os.path.expanduser('~/.ssh/known_hosts')))


def migrate():
    _put_envs()
    _update_settings()
    _update_virtualenv()
    _update_static_files()
    _update_database()
    _make_virtualhost()
    _grant_apache2()
    _restart_apache2()

def _put_envs():
    put('envs.json', '~/{}/envs.json'.format(PROJECT_NAME))
    #put('bank_envs.json', '~/{}/bank_envs.json'.format(PROJECT_NAME))

def _get_latest_apt():
    update_or_not = input('would you update?: [y/n]')
    if update_or_not=='y':
        sudo('sudo apt-get update && sudo apt-get -y upgrade')

def _install_apt_requirements(apt_requirements):
    reqs = ''
    for req in apt_requirements:
        reqs += (' ' + req)
    sudo('sudo apt-get -y install {}'.format(reqs))

def _make_virtualenv():
    if not exists('~/.virtualenvs'):
        script = '''"# python virtualenv settings
                    export WORKON_HOME=~/.virtualenvs
                    export VIRTUALENVWRAPPER_PYTHON="$(command \which python3)"  # location of python3
                    source /usr/local/bin/virtualenvwrapper.sh"'''
        run('mkdir ~/.virtualenvs')
        sudo('sudo pip3 install virtualenv virtualenvwrapper')
        run('echo {} >> ~/.bashrc'.format(script))


def _get_latest_source():
    if exists(project_folder + '/.git'):
        run('cd %s && git fetch' % (project_folder,))
    else:
        run('git clone %s %s' % (REPO_URL, project_folder))
    current_commit = local("git log -n 1 --format=%H", capture=True)
    run('cd %s && git reset --hard %s' % (project_folder, current_commit))

def _update_settings():
    settings_path = project_folder + '/{}/settings.py'.format(PROJECT_NAME)

    sed(settings_path, "DEBUG = True", "DEBUG = False")
    # sed(settings_path, "DEBUG = True", "DEBUG = True")

    sed(settings_path,
        'ALLOWED_HOSTS = .+$',
        'ALLOWED_HOSTS = ["%s"]' % (REMOTE_HOST,),

    )
    secret_key_file = project_folder + '/{}/secret_key.py'.format(PROJECT_NAME)

    if not exists(secret_key_file):
        chars = 'abcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*(-_=+)'
        key = ''.join(random.SystemRandom().choice(chars) for _ in range(50))
        append(secret_key_file, "SECRET_KEY = '%s'" % (key,))
    append(settings_path, '\nfrom .secret_key import SECRET_KEY')

def _update_virtualenv():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    if not exists(virtualenv_folder + '/bin/pip'):
        run('cd /home/%s/.virtualenvs && virtualenv %s' % (env.user, PROJECT_NAME))
    run('%s/bin/pip install -r %s/requirements.txt' % (
        virtualenv_folder, project_folder
    ))

def _update_static_files():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    run('cd %s && %s/bin/python3 manage.py collectstatic --noinput' % (
        project_folder, virtualenv_folder
    ))

def _update_database():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    run('cd %s && %s/bin/python3 manage.py migrate --noinput' % (
        project_folder, virtualenv_folder
    ))

def _ufw_allow():
    sudo("ufw allow 'Apache Full'")
    sudo("ufw reload")

def _make_virtualhost():
    script = """'<VirtualHost *:80>
    ServerName {servername}
    Alias /{static_url} /home/{username}/{project_name}/{static_root}
    Alias /{media_url} /home/{username}/{project_name}/{media_url}
    <Directory /home/{username}/{project_name}/{media_url}>
        Require all granted
    </Directory>
    <Directory /home/{username}/{project_name}/{static_root}>
        Require all granted
    </Directory>
    <Directory /home/{username}/{project_name}/{project_name}>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>
    WSGIDaemonProcess {project_name} python-home=/home/{username}/.virtualenvs/{project_name} python-path=/home/{username}/{project_name}
    WSGIProcessGroup {project_name}
    WSGIScriptAlias / /home/{username}/{project_name}/{project_name}/wsgi.py
    ErrorLog ${{APACHE_LOG_DIR}}/error.log
    CustomLog ${{APACHE_LOG_DIR}}/access.log combined
    </VirtualHost>'""".format(
        static_root=STATIC_ROOT_NAME,
        username=env.user,
        project_name=PROJECT_NAME,
        static_url=STATIC_URL_NAME,
        servername=REMOTE_HOST,
        media_url=MEDIA_ROOT
    )
    sudo('echo {} > /etc/apache2/sites-available/{}.conf'.format(script, PROJECT_NAME))
    sudo('a2ensite {}.conf'.format(PROJECT_NAME))

def _grant_apache2():
    sudo('chown :www-data ~/{}'.format(PROJECT_NAME))
    # enable below if use sqlite3
    sudo('chmod 775 ~/{}/db.sqlite3'.format(PROJECT_NAME))
    # sudo('chmod a+w ~/{}/db.sqlite3'.format(PROJECT_NAME))
def _restart_apache2():
    sudo('sudo service apache2 restart')

{% endhighlight %}

## 과정 
- gitignore 에 sqlite3 를 추가하여 데이터가 지워지지 않도록함.
- 실행하면 github의 유저네임, 비번을 입력하도록 하는 창이 계속 나타났음.
- 이때에는 서버의 .ssh/에 퍼블릭 키를 생성하고 이를 github에 등록하면됨. 또한 연결된 주소는 ssh 주소로 바꾸면 됨.
- 서버에서 git fetch에 대한 명령에 의해 나타남
- git 과 연결할때 가장 처음에는 ssh말고 그냥 주소로 해야함.
- staic_root 를 세팅파일에 추가해야 함.
- 서버에 ssh로 접속하여 서버에서 git 명령이 ssh로 나타나도록 설정하는 것이 중요(주소를 git에서 ssh형태로 복사 !서버에 .ssh가 있는 지 확인하였음)
- myg 를 통해 git push와 배포자동화 (명령 : fab myg:"pushname")
- 처음에 ssh 관련 오류가 나서, 주소를 ip주소로 바꾸니 됨.
- ssh 오류가 나서 .ssh/known_hosts를 지우니 해결됨.
- git reset --hard ***오류가 발생, 서버측에 git 장소를 제대로 지정하니 해결됨.
- 혹은 git push가 다되었는지 확인! 꼭!
- fatal: Could not read from remote repository.
Please make sure you have the correct access rights and the repository exists.
- 이 경우 서버에 직접 ssh키를 생성하고 서버에 생성된 공개키를 github에 등록하면 되었음.
- key_load_public: invalid format Permission denied (publickey). fatal: Could not read from remote repository.
- 위의 에러의 경우 서버에 직접 ssh키를 생성하고 서버에 생성된 공개키를 github에 등록하면 되었음. 이때 서버에 개인키가 있고 이것에 대한 공개키가 github에 있어야 하는 것 같음.
> https://beomi.github.io/2017/03/20/Deploy-Django-with-Fabric/
