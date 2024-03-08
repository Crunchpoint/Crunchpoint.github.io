---
layout: single
title: "[Linux & Flask] 클라우드 서버에서 메일 전송 구현"
categories: [linux]
tags: [python, linux, cloud, server, flask]
header:
  teaser: /assets/images/teasers/teaser_linux.webp
---

# 리눅스 환경에서 메일 전송 서버 구현하기 (flask 활용)

만약 클라우드 서버 구성이 되어있지 않다면, 아래의 링크를 참고하여 오라클 클라우드의 프리티어를 사용하여 인스턴스를 생성할 수 있습니다.

오라클 인스턴스 생성은 **[여기](http://localhost:4000/oracle/oracle-instance/){:target="\_blank"}**를 참고 해주세요

메일 서버를 구성하여 제 블로그의 contact 페이지에서 메일을 전송할 수 있도록 구현하였습니다.

## 1. 필요한 패키지 설치

```bash
$ sudo apt-get update
$ sudo apt-get install python3-pip
$ sudo pip3 install flask
$ sudo pip3 install flask-mail
```

## 2. 메일 전송 서버 구현

아래의 코드는 flask를 사용하여 메일 전송 서버를 구현한 코드입니다.

```python
from flask import Flask, request, redirect, url_for
from flask_mail import Mail, Message

# Flask-Mail 설정
app.config['MAIL_SERVER'] = 'smtp.gmail.com' # 메일 서버
app.config['MAIL_PORT'] = 587 # 메일 서버 포트
app.config['MAIL_USE_TLS'] = True # TLS 사용 여부
app.config['MAIL_USERNAME'] = 'address@gmail.com' # 메일 주소
app.config['MAIL_PASSWORD'] = 'app_password' # 앱 비밀번호

RECIPIENT_EMAIL = '' # 수신자 메일 주소

mail = Mail(app)

@app.route('/submit', methods=['POST'])
def submit():
    name = request.form.get('name') # form에서 name이라는 이름의 input 태그의 값을 가져옴
    email = request.form.get('email') # form에서 email이라는 이름의 input 태그의 값을 가져옴
    message = request.form.get('message') # form에서 message라는 이름의 input 태그의 값을 가져옴

    # 메일 메시지 생성
    sender_email = email
    msg = Message(subject=f"Message from {name}", # 메일 제목
                  sender=sender_email, # 발신자 메일 주소
                  recipients=[RECIPIENT_EMAIL], # 수신자 메일 주소
                  body=f"Name: {name}\nEmail: {email}\nMessage: {message}") # 메일 내용

    # 메일 전송
    mail.send(msg)

    return "메일 전송 완료"

if __name__ == "__main__":
   app.run(host="0.0.0.0", port=5000, debug=True)
```

## 3. form 구현

간단한 contact form을 작성하여, 이름과 발송자의 이메일 주소, 그리고 메시지를 입력하고 전송할 수 있도록 구현합니다.

```html
<form id="contact_form" class="contact_form" action="https://서버주소" method="POST">
  <div class="input_container">
    <input type="text" name="name" placeholder="Name" required />
    <input type="email" name="email" placeholder="Email" required />
  </div>
  <br />
  <textarea name="message" placeholder="Message" maxlength="500" required></textarea>
  <button class="btn" type="submit">Submit</button>
</form>

<script>
  const form = document.querySelector(".contact_form");

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    alert("메시지가 전송되었습니다. 감사합니다!");
    this.submit();
  });
</script>
```

## 4. 서버 실행

nohup명령어를 사용하여 백그라운드에서 서버를 실행합니다.

```bash
$ nohup sudo python3 app.py --port=5000 > output.log 2>&1 &
```

## 5. 문제점 및 해결 방법

1. https 보안 문제 관련해서 경고가 지속적으로 발생
   - 이 문제의 해결을 위해 무료 도메인 주소를 발급 받아서 nginx서버에 let's encrypt에서 발급받은 ssl 인증서를 적용하고 flask서버를 location으로 포워딩하여 해결하였습니다.

## 6. 개선 방향

1. 메일 전송 개선

   - 현 상태에서는 메일을 내가 나 자신한테 보내는 것으로 코드가 작성되어 있기 때문에 이를 개선하여 수신자의 메일 주소를 입력받아 메일을 전송할 수 있도록 개선할 예정입니다.
     ![mail](/assets/images/2024/2024-03-08/01.png)

2. 메일 서버의 보안 강화

- 메일 서버의 보안을 강화하여 스팸 메일을 방지하고, 보안 취약점을 보완하여 안전한 메일 전송 서버를 구축할 수 있도록 개선할 예정입니다.
