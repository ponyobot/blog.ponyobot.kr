# About
이 사이트는 포뇨의 개인 블로그입니다.

::github{repo="ponyobot/ponyobot"}

### 구동환경
```
Ubuntu(Docker)
  ↓
Redroid Android 14 (redroid/redroid:14.0.0-latest)
  ├── KakaoTalk (로그인/DB 생성)
  └── Iris APK (DB 폴링 → HTTP/WebSocket)
       ↓ dashboard:3000
Ubuntu 봇 서버 (iris_bot)
  ├── /ws 수신 (새 메시지 이벤트)
  └── /reply POST (답장 전송)
```

> - [Redroid](https://github.com/remote-android/redroid-doc)를 이용해 카카오톡/메세지전송부만 담당합니다
> - 메세지처리는 안드로이드 밖에서 담당합니다
> - [Iris](https://github.com/dolidolih/Iris)를 통해 메시지를 송수신을 한다
> - [Iris_bot](https://github.com/dolidolih/iris_bot)을 사용합니다

1. Iris란

    - 안드로이드 네이티브 DB기반 봇 프레임워크

### 라이브러리
> - [irispy-client](https://github.com/dolidolih/irispy-client)

> ### 이 사이트에 이용된 이미지의 출처
> - [봇 프로필](https://kr.pinterest.com/pin/580823683224569861)
> - [배경](https://kr.pinterest.com/pin/344595809003176087)