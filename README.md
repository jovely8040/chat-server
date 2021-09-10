## 프로젝트 폴더 생성
- chat-server

## 프로젝트 추가
- chat-server
- 약관 동의
- 애널리틱스 해제
- 프로젝트 만들기

## Firebase CLI 설치

```bash
$ npm install -g frirebase-tools
```

## Firebase CLI 로그인 / 로그아웃

```bash
// 로그인 + 구글 계정 인증
$ frirebase login

+ success! Logged in as xxx@gmail.com
```
```bash
// 로그아웃
$ frirebase logout
```
## Firebase 프로젝트 확인

```bash
$ firebase projects:list

√ Preparing the list of your Firebase projects
```

## Firebase 프로젝트 초기화
- 프로젝트에서 사용할 디렉토리 만들기
```bash
$ mkdir chat-server
$ cd chat-server
```

- 호스팅 설정
```bash
$ frirebase init hosting

? Are you ready to proceed? Yes

? Please select an option: Use an existing project

? Select a default Firebase project for this directory: 목록에서 해당하는 프로젝트 선택

? What do you want to use as your public directory? public

? Configure as a single-page app(rewrite all urls to / index.html)? N

? Set up automatic builds and deploys with GitHub? N

+  Firebase initialization complete!
```

- 펑션 설정
```bash
$ firebase init functions

? Are you ready to proceed? Yes

? What language would you like to use to write Cloud Functions? JavaScript 

? Do you want to use ESLint to catch probable bugs and enforce style? No

? Do you want to install dependencies with npm now? Yes

+ Firebase initialization complete!
```

- Firebase Database 설정
```bash
$ firebase init database

? Are you ready to proceed? Yes

? It seems like you haven’t initialized Realtime Database in your project yet. Do you want to set it up? Yes

? Please choose the location for your default Realtime Database instance: us-central1

? What file should be used for Realtime Database Security Rules? database.rules.json

+  Firebase initialization complete!
```

- Firebase Database 구축
```bash
// database.rules.json 파일
// false를 true로 설정
{
  /* Visit https://firebase.google.com/docs/database/security to learn more about security rules. */
  "rules": {
    ".read": true,
    ".write": true
  }
}
```
## 프로젝트 구축
```bash
$ firebase serve --only functions

+  Firebase initialization complete!

> 가상 서버 주소: http://localhost:5000/chat-server-6a35e/us-central1/v1
```
> 참고 소스 링크: https://raw.githubusercontent.com/okachijs/jsframeworkbook/master/2_5_server/functions/index.js
> 소스 복사 후 functions\index.js 파일에 붙여 넣기

### RESTful API 테스트
> GIT bash로 수행
```bash
// 서버 띄우기
$ firebase serve --only functions

+  functions[us-central1-v1]: http function initialized (http://localhost:5000/chat-server-6a35e/us-central1/v1).

// 채널 생성 API
$ curl -H 'Content-Type:application/json' -d '{"cname": "general"}' http://localhost:5000/chat-server-6a35e/us-central1/v1/channels

{"result":"ok"}

// 채널 목록 API
$ curl http://localhost:5000/chat-server-6a35e/us-central1/v1/channels

{"channels":["general"]}

// 데이터 베이스 초기화 API
$ curl -H 'Content-Type:application/json' -d '{}' http://localhost:5000/chat-server-6a35e/us-central1/v1/reset

{"result":"ok"}
```
> RESTful API 테스트 프로그램: POSTMAN
