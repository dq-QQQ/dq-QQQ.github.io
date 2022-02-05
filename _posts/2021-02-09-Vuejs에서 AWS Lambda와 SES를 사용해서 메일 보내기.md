---
title: Vuejs에서 AWS Lambda와 SES를 사용해서 메일 보내기
date: 2021-02-09 20:18:01
permalink: /:short_year-:month-:day/:title
categories: [Cloud, web/network]
tags: [AWS, Lambda, Vuejs, javascript, email]
---


# 보고 그대로 따라하기 쌉가능

## 0. 이 문서를 작성하는 이유

(요약: 블로그 잘못 읽으면 골로간다...)

![작성이유](/assets/img/Untitled 2.png)

처음 이메일 기능을 넣으려 했을 때 한 블로거의 글을 읽었습니다. 마지막 멘트까지 살펴본 결과 '아 그대로 따라하면 쉽게 할 수 있겠구나', '이 정도면 얼마 안걸리겠다' 생각하고 착수했습니다. 
하지만 이 글은 AWS Lambda 사용에 포커스를 맞추고 이메일링에 대해서는 크게 설명하지 않았습니다. 
때문에 오히려 이 블로그글을 보고 따라하다가 중간중간 많은 내용들이 생략되어 있어서 오히려 많이 헤맸습니다.
믿고 그대로 따라했다가 삽질을 많이 했지만, 이제는 오히려 이 목적을 직접 달성하기 위해 다시 글을 작성하게 되었습니다.

![기성룡좌 짤](https://ppss.kr/wp-content/uploads/2013/07/20130402_025303.png)

(~~답답하면 니가 직접 뛰던가~~ ~~ )

`AWS lambda, AWS SES, nodemailer, Vuejs를 활용한 이메일 전송 기능`에 대해 이 글만 보고 따라해도 충분할 정도로 정리해보겠습니다.
Go Go Go!




## 1. 왜 AWS lambda를 사용해야 할까?

메일 기능... 간단한 것 같으면서도 그렇게 간단하지만은 않은 기능.

이걸 EC2에 올려서 메일 전송만 해주기에는 너무 리소스 낭비이고, 그렇다고 프론트에서 정적으로 동작하게만 만드는 것도 애매하다.

이럴 때 쓰라고 있는게 `AWS의 Lambda 기능`이다.

> AWS lambda란 간단히 말해서 '함수' 단위의 deploy이다.

어떤 이벤트가 발생했을 때에만 필요한 함수들은 클라우드 서버에 deploy하면 시간당 과금을 묻게된다. 이 경우 서버 호출이 자주 발생하지 않는 경우 비효율적(a.k.a. 돈낭비)이다.

반면, AWS lambda를 사용하면 함수가 호출되는 횟수에 따라 과금이 부과되기 때문에 메일링 서비스 같이 자주 불리지 않는 함수들은 따로 떼내어 관리하면 더욱 경제적이고 효율적으로 서버를 운영할 수 있게 되는 장점이 있다.



(2021. 2월 기준, 지원하는 언어는 C#, Go, Java, `Javascript(node.js)`, Perl, PHP, Python, Ruby이다.)

이번에는 javascript를 활용해보았다. (중간에 javascript에 대한 부족한 이해력때문에 삽질을 많이해서 순간적으로 python으로 할까 고민했던 순간을 간신히 넘겼다 ;;;)



## 2. 로컬환경에서 먼저 테스트 해보기

### 2-1. 로컬에서 메일 보내기

먼저, `nodemailer` 와 `nodemailer-smtp-transport`라는 npm 라이브러리를 먼저 설치하고 아래 예제 파일을 `index.js` 로 저장한다.

```bash
$ npm install nodemailer
$ npm i nodemailer-smtp-transport
```

```jsx
// index.js
/*
출처: https://docs.aws.amazon.com/ko_kr/ses/latest/DeveloperGuide/examples-send-using-smtp.html
This code uses callbacks to handle asynchronous function responses.
It currently demonstrates using an async-await pattern.
AWS supports both the async-await and promises patterns.
For more information, see the following:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/calling-services-asynchronously.html
https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html
*/

"use strict";
const nodemailer = require("nodemailer");

// If you're using Amazon SES in a region other than US West (Oregon),
// replace email-smtp.us-west-2.amazonaws.com with the Amazon SES SMTP
// endpoint in the appropriate AWS Region.
const smtpEndpoint = "email-smtp.us-west-2.amazonaws.com";

// The port to use when connecting to the SMTP server.
const port = 587;

// Replace sender@example.com with your "From" address.
// This address must be verified with Amazon SES.
const senderAddress = "Mary Major <sender@example.com>";

// Replace recipient@example.com with a "To" address. If your account
// is still in the sandbox, this address must be verified. To specify
// multiple addresses, separate each address with a comma.
var toAddresses = "recipient@example.com";

// CC and BCC addresses. If your account is in the sandbox, these
// addresses have to be verified. To specify multiple addresses, separate
// each address with a comma.
var ccAddresses = "cc-recipient0@example.com,cc-recipient1@example.com";
var bccAddresses = "bcc-recipient@example.com";

// Replace smtp_username with your Amazon SES SMTP user name.
const smtpUsername = "AKIAIOSFODNN7EXAMPLE";

// Replace smtp_password with your Amazon SES SMTP password.
const smtpPassword = "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY";

// (Optional) the name of a configuration set to use for this message.
var configurationSet = "ConfigSet";

// The subject line of the email
var subject = "Amazon SES test (Nodemailer)";

// The email body for recipients with non-HTML email clients.
var body_text = `Amazon SES Test (Nodemailer)
---------------------------------
This email was sent through the Amazon SES SMTP interface using Nodemailer.
`;

// The body of the email for recipients whose email clients support HTML content.
var body_html = `<html>
<head></head>
<body>
  <h1>Amazon SES Test (Nodemailer)</h1>
  <p>This email was sent with <a href='https://aws.amazon.com/ses/'>Amazon SES</a>
        using <a href='https://nodemailer.com'>Nodemailer</a> for Node.js.</p>
</body>
</html>`;

// The message tags that you want to apply to the email.
var tag0 = "key0=value0";
var tag1 = "key1=value1";

async function main(){

  // Create the SMTP transport.
  let transporter = nodemailer.createTransport({
    host: smtpEndpoint,
    port: port,
    secure: false, // true for 465, false for other ports
    auth: {
      user: smtpUsername,
      pass: smtpPassword
    }
  });

  // Specify the fields in the email.
  let mailOptions = {
    from: senderAddress,
    to: toAddresses,
    subject: subject,
    cc: ccAddresses,
    bcc: bccAddresses,
    text: body_text,
    html: body_html,
    // Custom headers for configuration set and message tags.
    headers: {
      'X-SES-CONFIGURATION-SET': configurationSet,
      'X-SES-MESSAGE-TAGS': tag0,
      'X-SES-MESSAGE-TAGS': tag1
    }
  };

  // Send the email.
  let info = await transporter.sendMail(mailOptions)

  console.log("Message sent! Message ID: ", info.messageId);
}

main().catch(console.error);
```

각각의 변수들이 무엇을 뜻하는지는 주석에 자세히 달려있다.



먼저 간단하게 몇 가지만 살펴보자.

```jsx
// 1. aws-email region이다. 기본적으로 us-west로 설정되어있는데 서울은 email-stmp.ap-northeast-2이다.
const smtpEndpoint = "email-smtp.us-west-2.amazonaws.com";

// 2. 보안사항
const smtpUsername = "AXXXXXXXXXXXXXXXE";
// Replace smtp_password with your Amazon SES SMTP password.
const smtpPassword = "wXXXXXXXXXXXXXXXXXXEY";

/*
이메일을 접속하기 위해서는 보낼 이메일이 있어야한다. 
간단하게 자신의 이메일을 활용한다면 아이디와 비밀번호가 필요하다.
하지만 아이디와 비밀번호를 코드에 그대로 노출시키는 것은 보안에 좋지 않으므로,
AWS에서 제공하는 SES(~~요정)~~ 기능을 사용하여 username과 password를 사용할 수 있다.
*/
```



### 2-2. AWS SES SMTP사용하기

AWS의 SES(~~요정?~~)는 뭔가 약자로 쓰면 멋있고 복잡한 기능같지만 그 뜻을 보면 생각보다 친근(?)하다. Simple Email Service의 약자로 말그대로 간단한 email 서비스다. 

![SES](/assets/img/Untitled%203.png)

SES를 검색하고 클릭!

![email verify2](/assets/img/Untitled 4.png)

Email Address클릭!

![email verify2](/assets/img/Untitled 5.png)

email 인증 ㄱㄱ!

![AWS인증메일](/assets/img/Untitled 6.png)

*이 화면은 Gmail에서 AWS로부터 받은 메일 화면이다. 붉은 부분의 링크를 클릭하면 인증이 완료된다.*

![email verify3](/assets/img/Untitled 7.png)

*인증이 완료되면 pending verification이 `verified`로 변경된다.*

![email SMTP](/assets/img/Untitled 8.png)



인증이 완료되면 SMTP credentials를 생성한다.

이 과정을 거치면 `credentials.csv` 파일이 생성되고 이 파일을 다운로드 받아 열면 위의 `smtpUsername` 과 `smtpPassword`가 있으므로 index.js 파일의 해당 위치에 복붙한다.



여기까지 진행하고서 terminal에서 `node index` 를 입력하면 index.js가 실행되면서 내가 sendTo로 설정했던 메일로 메일이 날라가 있을 것이다.



## 3.  Lambda 사용해보기

### 3-1. AWS Lambda에서 함수 생성

![aws lambda1](/assets/img/Untitled 9.png)

*'Lambda 서버에 대한 걱정없이 코드 실행' 클릭*

![aws lambda2](/assets/img/Untitled 10.png)

*우상단 '함수 생성' 버튼 클릭*

![aws lambda3](/assets/img/Untitled%2011.png)

*함수이름, 런타임을 선택하고 함수생성 (이번에는 example이라는 함수명과 node14.x로 만들었습니다.)*

![aws lambda4](/assets/img/Untitled 12.png)

*트리거 추가 버튼 클릭*

![aws lambda5](/assets/img/Untitled 13.png)

*API 게이트웨이*

![aws gateway1](/assets/img/Untitled 14.png)

*보안 - 열기, CORS 체크는 일단 하지않고 놔두고 나중에 처리 ㄱㄱ*



아래로 내려와서 '함수 코드'쪽으로 내려온 뒤 index.js를 클릭해준다.

이 part가 lambda 함수를 작성하는 메인 공간이다.

![aws lambda6](/assets/img/Untitled 15.png)

*밝은 화면을 눈뜨고 지켜볼 수 없어 aws에서도 dark theme로 바꿔서 쓰는중이라 화면이 다르게 보일 수 있음 ;;*



간단한 예시 코드가 적혀있다

```jsx
exports.handler = async (event) => {
    // TODO implement
    const response = {
        statusCode: 200,
        body: JSON.stringify('Hello from Lambda!'),
    };
    return response;
};

람다는 이 exports.handler가 필수적이다. 
이후 response에 상태번호 200과 "hello from Lambda!"라는 문자열을 JSON으로 작성해 담아주고
이 response를 return해준다.

```

[handler에 대한 설명](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-handler.html)[영문]

Test버튼을 누르면 execution results 창이 나오면서 함수 실행 결과를 보여준다

![aws lambda7](/assets/img/Untitled 16.png)

성공적으로 통신이 된다면 Response에 statusCode와 Body에 문자열이 담겨있는 것을 확인할 수 있다.



### 3-2. AWS lamda에 로컬 환경과 똑같이 환경설정하기

![로컬파일트리](/assets/img/Untitled 17.png)

*로컬환경의 파일트리*

![lambda 파일트리](/assets/img/Untitled 18.png)

*AWS 람다 환경의 파일트리*



로컬 환경에서는 `npm`을 활용해서 nodemailer를 설치해 활용했다.

가장 문제는 이 라이브러리를 어떻게 aws 환경에서도 구성할 수 있을까였다.

AWS lambda에서 터미널을 찾아 헤맸지만 보이지 않아 이 부분에서 많이 당황했다.

해결방법은 생각보다 간단했다. 로컬의 이 디렉토리를 통째로 zip파일로 압축한 뒤 업로드하면 되는 것이었다.



[How to install npm modules in AWS Lambda?](https://www.youtube.com/watch?v=RnFowJ130pc)

이 유튜브 동영상을 보며 힌트를 얻고 따라할 수 있었다.

1. 로컬환경에서 zip 파일을 만든다.
2.  작업 버튼을 누르고 나오는 `.zip파일 업로드`로 압축해놓은 zip파일을 AWS에 올린다.

![index.js](/assets/img/Untitled 19.png)

(이렇게 쉬운 방법이 있었는데 하필 aws-sdk를 사용해 CLI환경에서 하는 방법이 구글링에서 먼저 나와 고생좀 했었다...ㅠ)

![업로드완료](/assets/img/Untitled 20.png)

이제 로컬 환경과 AWS lambda환경이 같아졌다. 여기까지 왔다면 거의 다왔다!



## 4. Vuejs로 이메일 전송 폼 만들기

### 4-1. .vue파일 만들기

```jsx
// Feedback.vue 전체 코드는 다음과 같다

<template>
  <div class="container">
    <h3>뉴하팀에 피드백 메일 보내기</h3>
    <v-form @submit.prevent="submit">
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="답장 받을 이메일"
        required
      ></v-text-field>

      <v-text-field
        v-model="title"
        label="제목"
        required
        autocapitalize="off"
      ></v-text-field>

      <v-textarea
        v-model="content"
        type="text"
        label="본문"
        required
      ></v-textarea>
      <br />
      <v-btn
        :disabled="!valid"
        color="#ff9800"
        @click="submit"
        >전송하기</v-btn
      >
    </v-form> 
  </div>
</template>

<script>
import axios from 'axios';
const API_FROM_AWS_API_GATEWAY = 'https://??????.ap-northeast-2.amazonaws.com/default/<함수명>';

export default {
  name: 'Feedback',
  methods: {
    isValid: function () {
      if (this.title == '' || this.content == '') {
        this.valid = false
      } else {
        this.valid = true
      }
    },
    submit: function () {
      axios.post(API_FROM_AWS_API_GATEWAY, JSON.stringify({
        email: this.email,
        title: this.title,
        content: this.content,
        }
      ))
      .then((res) => {
        console.log(res)
      })
      .catch((e) => {
        console.log(e)
      })
    },
  },
  data: function () {
    return {
      email: '',
      title: '',
      content: '',
      valid: false,
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }
  },
  watch: {
    title: function () {
      this.isValid();
    },
    content: function () {
      this.isValid();
    },
  }
}
</script>
```

1. v-form을 활용해 간단히 세 줄 짜리 input을 만들었다.
    - email
    - title
    - content
2. v-model로 email, title, content를 각각 입력받는 값을 string으로 binding했다.
3. AWS람다함수의 주소값을 넣어준다
4. axios를 import 한다

![주소1](/assets/img/Untitled%2021.png)

*lambda 화면에서 API게이트웨이를 클릭한다*

![주소2](/assets/img/Untitled 22.png)

이 붉은색 표시를 한 URL이 함수호출 게이트웨이값이다.

이 주소값을 const API_FROM_AWS_API_GATEWAY에 넣어준다.

```jsx
import axios from 'axios';
const API_FROM_AWS_API_GATEWAY = 'https://??????.ap-northeast-2.amazonaws.com/default/<함수명>';
```

5. submit 이라는 전송 함수를 methods에 추가한다.

- API 게이트웨이 주소로 POST방식의 axios 비동기 요청을 한다.

```jsx
submit: function () {
    axios.post(API_FROM_AWS_API_GATEWAY, JSON.stringify({
      email: this.email,
      title: this.title,
      content: this.content,
      }
    ))
    .then((res) => {
      console.log(res)
    })
    .catch((e) => {
      console.log(e)
    })
  },
},
```

여기까지 진행하고 크롬의 console창을 열어보면 status:200의 메시지가 도착해 있을 것으로 기대를 했겠지만 

크흠....역시나 한 번에 되지 않는다.



## 5. CORS 허용해주기

API Gateway에서 CORS를 허용해 줘야한다. 

![CORS](/assets/img/Untitled 23.png)

*CORS 클릭*

![CORS2](/assets/img/Untitled 24.png)

![CORS3](/assets/img/Untitled 25.png)



첫 번째 input창에 원하는 주소값을 넣어준다. 예시로는 http://[localhost:8080](http://localhost:8080) 을 추가한 모습인데, 

> 주의! 👏
> **마지막에 '/'슬래시를 붙이지 않는다.**

이유까지는 잘 모르겠지만  http://[localhost:8080](http://localhost:8080)/ 과 같은 형태로 했을 때 잘 작동하지 않는 문제가 있으니 이 점을 꼭 유의한다.

이렇게 하고 다시 폼을 전송해보면 반가운 statusCode 200을 받을 수 있을 것이다.

여기까지 성공했다면 거의 막바지에 다다랐다.



## 6. index.js 정리

### 6-1 event handler

현재 `index.js` 파일은 AWS제공해주는 기본 형식 그대로일 것이다.

하지만 Lambda에서 event가 발생하고 이것을 핸들하기 위해서는 event handler가 반드시 필요하다

따라서 시작 부분을 

'exports.handler = async (event, callback) => {'

와 같이 수정해준다.



### 6-2. 기타 설정하기

아래 완성된 코드 예시를 보면서 자신에게 맞도록 설정된 변수 값들을 수정해준다.

👏**이때 반드시 주의할 점은 시작은 exports.handler로 열어주고, 마지막은 꼭 return값을 넣어주도록 한다.**
(handler 스코프 바깥쪽에 변수같은건 설정 가능하다)

```jsx
exports.handler = async (event, callback) => {
---
let info = transporter.sendMail(mailOptions);   // 메일을 전송하는 마지막 코드
return info;     // 그리고 마지막에 return해줘야 함수가 제대로 실행된다.
}
```



### 6-3. 완성 코드 예시

```jsx
exports.handler = async (event, callback) => {
  // "use strict";
  const nodemailer = require("nodemailer");
  const smtpTransport = require('nodemailer-smtp-transport');

  // If you're using Amazon SES in a region other than US West (Oregon),
  // replace email-smtp.us-west-2.amazonaws.com with the Amazon SES SMTP
  // endpoint in the appropriate AWS Region.
  const smtpEndpoint = "email-smtp.ap-northeast-2.amazonaws.com"; // 서울 region을 사용하고 있다면 그대로 써도 좋다.
  
  // The port to use when connecting to the SMTP server.
  const port = 587;
  
  // Replace sender@example.com with your "From" address.
  // This address must be verified with Amazon SES.
  const senderAddress = "----@gmail.com";
  
  // Replace recipient@example.com with a "To" address. If your account
  // is still in the sandbox, this address must be verified. To specify
  // multiple addresses, separate each address with a comma.
  var toAddresses = "----@gmail.com";
  
  // Replace smtp_username with your Amazon SES SMTP user name.
  const smtpUsername = "AXXXXXXXXXXXXE";
  
  // Replace smtp_password with your Amazon SES SMTP password.
  const smtpPassword = "BXXXXXXXXXXXXXXXXXXXXXXO";
  
  // The subject line of the email
  
  // The email body for recipients with non-HTML email clients.
  
  
  const base64body = JSON.stringify(event.body)
  const body = JSON.parse(Buffer.from(base64body, 'base64').toString('utf8'))
  const data = {
    email: body.email,
    title: body.title,
    content: body.content,
  }
  var subject = `${data.title}`;
  var body_text = `${data.content}`;
  // The body of the email for recipients whose email clients support HTML content.
  var body_html = `<html>
  <head></head>
  <body>
    <h2> ${data.email} 님으로부터 NewsHi 피드백이 도착했습니다.</h2>
    <p> ${data.content}</p>
  </body>
  </html>`;
  
  // The message tags that you want to apply to the email.
  var tag0 = "key0=value0";
  var tag1 = "key1=value1";
  

  // Create the SMTP transport.
  let transporter = nodemailer.createTransport(smtpTransport({
    host: smtpEndpoint,
    port: port,
    secure: false, // true for 465, false for other ports
    auth: {
      user: smtpUsername,
      pass: smtpPassword
    }
  }));

  // Specify the fields in the email.
  let mailOptions = {
    from: senderAddress,
    to: toAddresses,
    subject: subject,
    text: body_text,
    html: body_html,
    service: "Gmail",
    // Custom headers for configuration set and message tags.
    headers: {
      'X-SES-MESSAGE-TAGS': tag0,
      'X-SES-MESSAGE-TAGS': tag1
    }
  };
  // Send the email.
  // let info = await transporter.sendMail(mailOptions);
  
  let info = transporter.sendMail(mailOptions);
  return info;
}
```

*<완성 모습>*

![완성1](/assets/img/Untitled.png)

*사이트에서 이메일 작성하는 폼*

![완성2](/assets/img/mailcomplete.png)

*G메일로 날아오는 결과*



끝.

---

### References.

**웬만하면 이 순서대로 참고하는 것을 추천.**

**특히, 마지막에 있는 velog 블로그 글은 꼭 마지막에 읽을 것을 추천함.**

[Amazon SES SMTP 인터페이스를 사용하여 이메일 전송](https://docs.aws.amazon.com/ko_kr/ses/latest/DeveloperGuide/examples-send-using-smtp.html)

[Amazon SES SMTP 인터페이스를 사용하여 이메일 전송](https://docs.aws.amazon.com/ko_kr/ses/latest/DeveloperGuide/examples-send-using-smtp.html)

[AWS Lambda 배포 패키지(Node.js)](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/nodejs-package.html)

[AWS Lambda 함수 핸들러(Node.js)](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/nodejs-handler.html)

[Sending email with Nodemailer using a lambda - Edward Beazer Blog](https://www.edwardbeazer.com/sending-email-using-nodemailer-using-a-lambda/)

[How to load npm modules in AWS Lambda?](https://stackoverflow.com/questions/34437900/how-to-load-npm-modules-in-aws-lambda)

[Vue.js와 AWS Lambda, Nodemailer 로 이메일 전송 폼 만들기](https://velog.io/@bluestragglr/Vue.js%EC%99%80-AWS-Lambda-Nodemailer-%EB%A1%9C-%EC%9D%B4%EB%A9%94%EC%9D%BC-%EC%A0%84%EC%86%A1-%ED%8F%BC-%EB%A7%8C%EB%93%A4%EA%B8%B0)