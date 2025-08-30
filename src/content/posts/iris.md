---
title: iris 설치하기
published: 2025-01-03
description: '안드로이드 네이티브 DB기반 봇 프레임워크'
image: ''
tags: [개인정보처리방침,프로그래밍,카카오톡 봇]
category: '카카오톡 봇'
draft: false
---

## 목차

- [1. Hyper-V 설치](#1-hyper-v-설치)
- [2. VM 생성](#2-vm-생성)
- [3. Ubuntu 설치](#3-ubuntu-설치)
- [4. IP 고정하기](#4-ip-고정하기)
- [5. Redroid 설치](#5-redroid-설치)
- [6. Iris 설치](#6-iris-설치)
- [7. 실행 - 서비스로 실행](#7-실행---서비스로-실행)
- [8. 실행 - 디버그모드로 실행](#8-실행---디버그모드로-실행)
- [9. 설정](#9-설정)
- [10. iris_bot 실행하기](#10-iris_bot-실행하기)

---

## Iris

> 본 가이드에서는 redroid 환경을 소개하고 있으며, android adb의 특성 상 "인증"이 없으므로,
> `공인IP가 외부에 노출된 서버환경에서 설치 시(예: 공유기 X)에는 추가적인 접근제어를 반드시 적용하여야 합니다.`


Iris가 동작하는 환경은 Android 9 이상의 루팅된 안드로이드 환경입니다.

따라서, 루팅된 휴대폰, 태블릿, 앱플레이어, Redroid 등등 대부분 환경에서 작동합니다.

(휴대폰, 태블릿의 루팅은 각자 진행하시고 [휴대폰에서 irispy-client 봇 돌리기](https://www.youtube.com/watch?v=pXWSU38PYl0) 영상을 참조 바랍니다.)

​
이 중 Redroid는 기본적으로 root 권한을 바로 사용할 수 있고, 안드로이드 쉘에 진입하지 않아도 안드로이드 외부에서 내부의 파일을 마음대로 액세스 할 수 있는 장점이 있습니다.

Windows에서 Redroid를 설치하는 것은 Windows의 무거움때문에 추천하지는 않으나,

리눅스를 메인호스트로 두면 어려움을 겪는 분들이 계셔서 Windows에서 가장 쉬운 설치법을 안내합니다.

(VMware, virtualbox 를 이용하여 VM을 만드는것도 가능하고, 굳이 Redroid를 사용하지 않고 AVD를 통해 리눅스 VM 없이 안드로이드 인스턴스를 이용하는 방법도 가능하고, 안드 9 이상 App player들을 이용하는것도 가능합니다.)

`우분투를 메인호스트로 설치해두었다면 1,2,3,4번은 스킵하고 5번부터 시작하시면 됩니다.`

> 자세한 내용은 iris 설치 가이드 영상을 확인해주세요.
- [iris 설치 가이드 영상](https://www.youtube.com/watch?v=H43VTOsKDXY)
> 
> iris 문서를 확인하세요.
- [iris 문서](https://kbotdocs.dev/reference/iris)
>
> iris, iris_bot, 가이드 영상 제작자 [돌다리](https://github.com/dolidolih)님
>
> iris 문서 제작자 [nolbo](https://github.com/kbotdocs)님

---

### 1. Hyper-v 설치

**※ Home 버전 윈도우는 아래 링크 참조**
- [윈도우10 Home 버전에서 Hyper-V(가상화 머신) 사용하기](https://m.blog.naver.com/toruin84/221936206258)

1. Professional 버전 윈도우는 Win+R 키를 누른 후 appwiz.cpl을 입력합니다.

2. Windows 기능 켜기/끄기를 선택합니다.

3. Hyper-V를 선택하고 확인을 누릅니다.

---

### 2. VM 생성

1. Hyper-V 관리자를 실행합니다.

2. 새로 만들기 -> 가상컴퓨터를 선택합니다.

3. 가상컴퓨터 설정을 하고 마침을 누르면 VM생성이 완료됩니다.

> - 이름 : redroid
> - 세대 : 2세대
> - 메모리 : 최소 4Gb 이상(8Gb 권장)
> - 네트워크 : Default Switch
> - 가상하드디스크 : 기본설정
> - 설치옵션 : 부팅 가능 CD/DVD-ROM에서 운영체제 설치 - 다운로드 받은 ubuntu 서버 이미지
- [ubuntu 서버 이미지 다운로드](https://mirror.kakao.com/ubuntu-releases/24.04.2/)

**※ ubuntu-24.04.3-live-server-amd64.iso를 다운로드 합니다**

4. 보안부팅 해제 후 시작

> - 설정 - 보안 - 보안부팅 사용 해제
> - 적용
> - 시작

---

### 3. Ubuntu 설치

1. 부팅메뉴가 등장하면 Try or Install Ubuntu를 선택합니다.

2. English 선택

3. Continue without  updating 선택

4. Keyboard 설정 변경없음

5. Ubuntu Server(기본) 선택

6. 네트워크 DHCP 선택. 이때 화면에 나타나는 IP를 기억해두세요.

7. Proxy 빈칸 엔터

8. Mirror 설정 http://mirror.kakao.com/ubuntu/ 로 변경

9. Use Entire disk 선택(기본)

10. 파티션 요약화면 엔터 후 Continue 선택

11. 이름, hostname, username, 비밀번호 설정

12. Ubuntu Pro는 skip for now

13. Install OpenSSH Server 선택

14. 추가패키지 아무것도 체크하지 않음.

15. Reboot Now 가 뜨면 엔터 후 미디어를 꺼내라고 하면 상단 메뉴의 미디어 - DVD 꺼내기 선택 후 엔터

16. 부팅이 완료되었다면 X를 눌러 콘솔화면을 종료합니다.(콘솔화면을 종료해도 VM이 꺼지지 않습니다.)

17. Windows 터미널에서 ssh로 접속합니다.(VM 내에서 작업은 불편합니다)

6번 절차에서 IP를 기억해두지 않았다면 VM에 로그인하면 인사메세지에 IP가 보입니다.

---

### 4. IP 고정하기

1. Hyper-V에서 Internal Switch 만들기

Hyper-V 관리자 실행

오른쪽 메뉴 → 가상 스위치 관리자 클릭

내부(Internal) 선택 후 새로 만들기 → 이름은 아무거나 지정후 저장

이러면 윈도우 네트워크 어댑터 목록에 vEthernet (스위치 이름) 라는 가상 어댑터가 생겨요.
(제어판 → 네트워크 및 공유센터 → 어댑터 설정 변경에서 확인 가능)

2. 윈도우에서 인터넷 공유 켜기

이제 호스트(윈도우) 네트워크를 VM에 공유해야 합니다.

윈도우에서 현재 인터넷 연결 중인 어댑터(예: Wi-Fi) 오른쪽 클릭 → 속성

공유 탭 클릭

다른 네트워크 사용자가 이 컴퓨터의 인터넷 연결을 통해 연결할 수 있도록 허용 체크

"홈 네트워킹 연결" 드롭다운에서 만들어둔 가상 어댑터 선택

확인

이렇게 하면 윈도우가 NAT 라우터처럼 동작해서 가상 어댑터 쪽으로도 인터넷을 뿌려줍니다.

3. Ubuntu VM에 고정 IP 설정하기

VM의 네트워크 어댑터를 만들어둔 가상 어댑터를 연결한 뒤, Ubuntu에서 직접 고정 IP를 줍니다.

VM 설정 → 네트워크 어댑터 → 만들어둔 가상 어댑터 선택

ssh에 연결해 네트워크 설정 파일 편집

```
sudo nano /etc/netplan/01-netcfg.yaml
```
안에 아래 내용 넣기

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.137.2/24
      routes:
        - to: default
          via: 192.168.137.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1
```
ctrl + x 누르고 y 누르면 저장이 되고 아래 명령어를 입력해 저장한다

```
sudo netplan apply
```

이렇게 하면 ssh 연결할때 `ssh 192.168.137.2`로 연결 가능

### 5. Redroid 설치

1. iris_control을 다운로드 받습니다.

```
wget https://github.com/dolidolih/Iris/releases/latest/download/iris_control
chmod +x iris_control
```

2. iris_control을 이용하여 redroid를 설치합니다.

```
./iris_control install_redroid
```

3. 다른 터미널 창을 열어 adb, scrcpy로 접속합니다.
- [scrcpy 다운로드](https://github.com/Genymobile/scrcpy/releases/tag/v3.1)

> - Windows (64비트 대부분 PC) → scrcpy-win64-v3.1.zip
> - Windows (32비트 PC) → scrcpy-win32-v3.1.zip
> - Linux (x86_64, 일반적인 데스크탑/노트북용 리눅스) → scrcpy-linux-x86_64-v3.1.tar.gz
> - macOS (Intel CPU, x86_64) → scrcpy-macos-x86_64-v3.1.tar.gz
> - macOS (M1/M2/M3 같은 Apple Silicon, aarch64) → scrcpy-macos-aarch64-v3.1.tar.gz

```
#scrcpy가 설치된 폴더로 이동
cd ~
./adb connect 봇IP
./scrcpy -s 봇IP
```

4. 카카오톡 설치

split apk로 나오고 있어서 apkpure 등에서 xapk 등등을 받은 후 파일명 뒤에 .zip을 붙이고 압축을 해제합니다.

```
adb -s BOTIP install-multiple (get-item *.apk)
```

좀 더 쉬운방법
> - apkpure 등에서 xapk 등 다운로드 합니다
> - Microsoft Store 에서 App Installer (Mobile) - WinUI 3을 다운로드 합니다
> - 설정버튼에 들어가 redroid_x86_64 클릭, For WSA only? 해제, 뒤로가기 합니다
> - 카톡이 설치가 되면 scrcpy가 끊어질 건데 다시 접속해 주면 됩니다.

- [App Installer (Mobile) - WinUI 3 다운로드](https://apps.microsoft.com/detail/9P2JFQ43FPPG?hl=neutral&gl=KR&ocid=pdpshare)

---

### 6. Iris 설치

ssh 연결된 터미널에서 다음과 같이 입력합니다.

```
sudo apt install adb
adb connect 봇IP
./iris_control install
```

---

### 7. 실행 - 서비스로 실행

```
adb connect 봇IP
./iris_control start
./iris_control status
./iris_control stop
```

위 세가지 기능을 통해 시작/확인/정지가 가능합니다.

​---

### 8. 실행 - 디버그모드로 실행

```
adb shell
su
app_process /data/local/tmp/Iris.apk / party.qwer.iris.Main
```

위의 방법으로 실행하면 로그를 실시간으로 확인할 수 있고, Ctrl+C를 눌러 종료하는 즉시 Iris가 종료됩니다.

---

### 9. 설정

윈도우 컴퓨터의 인터넷 브라우저에서 아래 주소에 접속합니다.

- http://BOTIP:3000/dashboard

---

### 10 iris_bot 실행하기

**※ 자세한 내용은 https://github.com/dolidolih/iris_bot 을 확인하세요**

1. 저장소 복제 및 Python 가상 환경 설정: 터미널에서 다음 명령어를 실행하세요
```
cd ~
git clone https://github.com/dolidolih/iris_bot
cd iris_bot
python -m venv venv

# 가상 환경 활성화 (Windows의 경우 venv/Scripts/Activate.ps1)
source venv/bin/activate

pip install -U pip
pip install -r requirements.txt

iris init
``` 

2. Admin User ID 설정

```
iris admin add <user_id>
```

3. KakaoLink 설정(Optional)

```
iris kakaolink <app_key> <origin>
```

4. 서비스 설정(Optional)

```
iris service create
iris service start/stop/status
```


---

