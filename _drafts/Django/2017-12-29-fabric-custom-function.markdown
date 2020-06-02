---
# layout: "post"
title: "fabric custom function"
date: "2017-12-29 00:19"
# categories: "Django"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "Django"
slug: "fabric_custom_function"
header:
  teaser: /assets/images/9.png

---

``` python
def myg(val="blank"):
    '''git push하고 배포 이거는 전체를 다시올리는 것이라 데이타 베이스가 다 초기화됨'''
    local('git add .')
    local('git commit -m {}'.format(val))
    local('git push')
    deploy()

def edit(startfolder,endfolder):
    '''해당폴더를 업로드, 해당폴더만 찍어서 업로드함. 폴더명에 주의해야 함. 있는 폴더는 합쳐짐(완전히 똑같아지는 게 아니라 합해지는 것 같음.)
    scp -r ./testfolder idroot@example.com:/home/hvofak5s
    fab edit:"./test",""
    '''
    local('scp -r {} idroot@example.com:/home/hvofak5s/{}'.format(startfolder,endfolder))
    sudo('sudo service apache2 restart')
```

- myg 는 git push 후 전체를 다 배포함. 데이터베이스가 전부초기화되는 등 비효율적임.
- edit은 필요한 폴더만 올림. 이때 A라는 폴더를 A위치에 올리면, 두개의 내용이 합쳐짐. 단, 같은 제목의 파일은 덮어씀.이부분을 주의해야함
- 그 외의 migration등은 fabfile의 내용을 참고하여 쓸 수 있음.
- edit의 경우 위치를 잘지정해야 함.
- fab edit:"./test","" 하면, test폴더가 /home/hvofak5s/test 로 옮겨짐.
