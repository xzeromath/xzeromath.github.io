---
layout: post
title: 테스트
date: 2017-02-08 12:29:37.000000000 +09:00
# type: post
# status: publish
categories:
# - Etc
tag:
- Etc
---


import mechanicalsoup



```python
browser = mechanicalsoup.StatefulBrowser()
```


```python
browser.open("https://nid.naver.com/nidlogin.login")
```


fakfa

    <Response [200]>




```python
browser.select_form('form[action="https://nid.naver.com/nidlogin.login"]')
```




    <mechanicalsoup.form.Form at 0x113559128>




```python
browser.get_current_page().find_all('form')
```




    [<form action="https://nid.naver.com/nidlogin.login" autocomplete="off" id="frmNIDLogin" method="post" name="frmNIDLogin" onsubmit="return confirmSubmit();" target="_top">
     <input id="enctp" name="enctp" type="hidden" value="2"/>
     <input id="encpw" name="encpw" type="hidden" value=""/>
     <input id="encnm" name="encnm" type="hidden" value=""/>
     <input id="svctype" name="svctype" type="hidden" value="0"/>
     <input id="svc" name="svc" type="hidden" value=""/>
     <input id="viewtype" name="viewtype" type="hidden" value="0"/>
     <input id="locale" name="locale" type="hidden" value="ko_KR"/>
     <input id="postDataKey" name="postDataKey" type="hidden" value=""/>
     <input id="smart_LEVEL" name="smart_LEVEL" type="hidden" value="-1"/>
     <input id="logintp" name="logintp" type="hidden" value=""/>
     <input id="url" name="url" type="hidden" value="http://www.naver.com"/>
     <input id="localechange" name="localechange" type="hidden" value=""/>
     <input id="theme_mode" name="theme_mode" type="hidden" value=""/>
     <input id="ls" name="ls" type="hidden" value=""/>
     <input id="xid" name="xid" type="hidden" value=""/>
     <input id="pre_id" name="pre_id" type="hidden" value=""/>
     <input id="resp" name="resp" type="hidden" value=""/>
     <input id="exp" name="exp" type="hidden" value=""/>
     <input id="ru" name="ru" type="hidden" value=""/>
     <fieldset class="login_form">
     <legend class="blind">로그인</legend>
     <div class="input_row" id="id_area">
     <span class="input_box">
     <label class="lbl" for="id" id="label_id_area">아이디</label>
     <input accesskey="L" class="int" id="id" maxlength="41" name="id" placeholder="아이디" tabindex="7" type="text" value=""/>
     </span>
     <button class="wrg" disabled="" id="id_clear" title="delete" type="button">삭제</button>
     </div>
     <div class="error" id="err_empty_id" style="display:none;">아이디를 입력해주세요.</div>
     <div class="input_row" id="pw_area">
     <span class="input_box">
     <label class="lbl" for="pw" id="label_pw_area">비밀번호</label>
     <input class="int" id="pw" maxlength="16" name="pw" onkeydown="checkShiftDown(event);" onkeypress="capslockevt(event);getKeysv2();" onkeyup="checkShiftUp(event);" placeholder="비밀번호" tabindex="8" type="password"/>
     </span>
     <button class="wrg" disabled="" id="pw_clear" title="delete" type="button">삭제</button>
     <div class="ly_v2" id="err_capslock" style="display:none;">
     <div class="ly_box">
     <p><strong>Caps Lock</strong>이 켜져 있습니다.</p> </div>
     <span class="sp ly_point"></span>
     </div>
     </div>
     <div class="error" id="err_empty_pw" style="display:none;">비밀번호를 입력해주세요.</div>
     <input alt="로그인" class="btn_global" onclick="nclks('log.login',this,event)" tabindex="12" title="로그인" type="submit" value="로그인"/>
     <div class="check_info">
     <div class="login_check">
     <span class="login_check_box">
     <input class="" id="login_chk" name="nvlong" onchange="savedLong(this);nclks_chk('login_chk', 'log.keepon', 'log.keepoff',this,event)" tabindex="9" type="checkbox" value="off"/>
     <label class="sp" for="login_chk" id="label_login_chk">로그인 상태 유지</label>
     </span>
     <div class="ly_v2" id="persist_usage" style="display:none;">
     <div class="ly_box">
     <p>개인정보 보호를 위해 <strong>개인 PC에서만 사용하세요.</strong>  <a class="sp btn_check_help" href="https://help.naver.com/support/contents/contents.nhn?serviceNo=532&amp;categoryNo=1523" target="_blank">도움말보기</a></p>
     </div>
     <span class="sp ly_point"></span>
     </div>
     </div>
     <div class="pc_check">
     <span class="ip_check">
     <a href="/login/ext/help_ip3.html" onclick="window.open(this.href, 'IPGUIDE', 'titlebar=1, resizable=1, scrollbars=yes, width=537, height=750'); return false;" tabindex="10" target="_blank" title="">IP보안</a>
     <span class="ip_ch">
     <input checked="checked" class="" id="ip_on" onchange="ipCheck(this,event);nclks_chk('ip_on', 'log.iponset', 'log.ipoffset',this,event)" tabindex="11" type="checkbox"/>
     <label class="sp" for="ip_on" id="label_ip_on">on</label>
     </span>
     </span>
     <span class="bar">|</span>
     <span class="dis_di">
     <a href="#" onclick="onetime(); nclks('log.otn',this,event); return false;" title="일회용 로그인">일회용 로그인</a><a class="sp btn_help" href="javascript:viewOnetime();" onclick="nclks('log.otnhelp',this,event)" title="도움말">도움말</a>
     <div class="ly" id="onetime_usage" onclick="javascript:viewOnetime()" style="display:none;">
     <div class="ly_box">
     <p>네이버앱에서 생성된 일회용 로그인 번호를 입력하면, 앱에 로그인된 계정으로 PC에서 로그인할 수 있어요. 아이디/비밀번호를 입력하지 않아 간편하고 더욱 안전합니다.</p> </div>
     <span class="sp ly_point"></span>
     </div>
     </span>
     </div>
     </div>
     </fieldset>
     </form>]




```python
browser.get_current_form().print_summary()
```

    <input id="enctp" name="enctp" type="hidden" value="2"/>
    <input id="encpw" name="encpw" type="hidden" value=""/>
    <input id="encnm" name="encnm" type="hidden" value=""/>
    <input id="svctype" name="svctype" type="hidden" value="0"/>
    <input id="svc" name="svc" type="hidden" value=""/>
    <input id="viewtype" name="viewtype" type="hidden" value="0"/>
    <input id="locale" name="locale" type="hidden" value="ko_KR"/>
    <input id="postDataKey" name="postDataKey" type="hidden" value=""/>
    <input id="smart_LEVEL" name="smart_LEVEL" type="hidden" value="-1"/>
    <input id="logintp" name="logintp" type="hidden" value=""/>
    <input id="url" name="url" type="hidden" value="http://www.naver.com"/>
    <input id="localechange" name="localechange" type="hidden" value=""/>
    <input id="theme_mode" name="theme_mode" type="hidden" value=""/>
    <input id="ls" name="ls" type="hidden" value=""/>
    <input id="xid" name="xid" type="hidden" value=""/>
    <input id="pre_id" name="pre_id" type="hidden" value=""/>
    <input id="resp" name="resp" type="hidden" value=""/>
    <input id="exp" name="exp" type="hidden" value=""/>
    <input id="ru" name="ru" type="hidden" value=""/>
    <input accesskey="L" class="int" id="id" maxlength="41" name="id" placeholder="아이디" tabindex="7" type="text" value=""/>
    <input class="int" id="pw" maxlength="16" name="pw" onkeydown="checkShiftDown(event);" onkeypress="capslockevt(event);getKeysv2();" onkeyup="checkShiftUp(event);" placeholder="비밀번호" tabindex="8" type="password"/>
    <input alt="로그인" class="btn_global" onclick="nclks('log.login',this,event)" tabindex="12" title="로그인" type="submit" value="로그인"/>
    <input class="" id="login_chk" name="nvlong" onchange="savedLong(this);nclks_chk('login_chk', 'log.keepon', 'log.keepoff',this,event)" tabindex="9" type="checkbox" value="off"/>
    <input checked="checked" class="" id="ip_on" onchange="ipCheck(this,event);nclks_chk('ip_on', 'log.iponset', 'log.ipoffset',this,event)" tabindex="11" type="checkbox"/>



```python
browser['id']='hvofak5s'
```


```python
browser['pw']='naver112629'
```


```python
browser.get_current_form().print_summary()
```

    <input id="enctp" name="enctp" type="hidden" value="2"/>
    <input id="encpw" name="encpw" type="hidden" value=""/>
    <input id="encnm" name="encnm" type="hidden" value=""/>
    <input id="svctype" name="svctype" type="hidden" value="0"/>
    <input id="svc" name="svc" type="hidden" value=""/>
    <input id="viewtype" name="viewtype" type="hidden" value="0"/>
    <input id="locale" name="locale" type="hidden" value="ko_KR"/>
    <input id="postDataKey" name="postDataKey" type="hidden" value=""/>
    <input id="smart_LEVEL" name="smart_LEVEL" type="hidden" value="-1"/>
    <input id="logintp" name="logintp" type="hidden" value=""/>
    <input id="url" name="url" type="hidden" value="http://www.naver.com"/>
    <input id="localechange" name="localechange" type="hidden" value=""/>
    <input id="theme_mode" name="theme_mode" type="hidden" value=""/>
    <input id="ls" name="ls" type="hidden" value=""/>
    <input id="xid" name="xid" type="hidden" value=""/>
    <input id="pre_id" name="pre_id" type="hidden" value=""/>
    <input id="resp" name="resp" type="hidden" value=""/>
    <input id="exp" name="exp" type="hidden" value=""/>
    <input id="ru" name="ru" type="hidden" value=""/>
    <input accesskey="L" class="int" id="id" maxlength="41" name="id" placeholder="아이디" tabindex="7" type="text" value="hvofak5s"/>
    <input class="int" id="pw" maxlength="16" name="pw" onkeydown="checkShiftDown(event);" onkeypress="capslockevt(event);getKeysv2();" onkeyup="checkShiftUp(event);" placeholder="비밀번호" tabindex="8" type="password" value="naver112629"/>
    <input alt="로그인" class="btn_global" onclick="nclks('log.login',this,event)" tabindex="12" title="로그인" type="submit" value="로그인"/>
    <input class="" id="login_chk" name="nvlong" onchange="savedLong(this);nclks_chk('login_chk', 'log.keepon', 'log.keepoff',this,event)" tabindex="9" type="checkbox" value="off"/>
    <input checked="checked" class="" id="ip_on" onchange="ipCheck(this,event);nclks_chk('ip_on', 'log.iponset', 'log.ipoffset',this,event)" tabindex="11" type="checkbox"/>



```python
response = browser.submit_selected()
```


```python
print(response.text)
```

    <html>
    <script language=javascript>
    location.replace("https://nid.naver.com/login/sso/finalize.nhn?url=http%3A%2F%2Fwww.naver.com&sid=vVPdbiNrvNcts6Z3&svctype=1");
    </script>
    </html>



### 실패


```python
browser.launch_browser()
```


```python

```
