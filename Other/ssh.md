# SSH(Secure Shell)란?
GitHub에서 코드를 올리거나 서버에 접속하다 보면 `SSH Key`를 만들라는 안내를 자주 보게 된다. <br>

그런데 SSH와 SSH Key를 같은 개념으로 생각하는 경우가 많다.

사실 두 개는 서로 다른 개념이다.
- SSH는 컴퓨터끼리 안전하게 통신하기 위한 프로토콜이다.
- SSH Key는 SSH에서 사용할 수 있는 사용자 인증 방법 중 하나다.

이번 글에서는 먼저 SSH가 왜 만들어졌고, 어떤 문제를 해결하는지 알아보자.

## SSH는 무엇일까?
SSH(Secure Shell)는 **인터넷에서 다른 컴퓨터와 안전하게 통신하기 위한 암호화 프로토콜**이다.

쉽게 말해, 인터넷을 통해 다른 컴퓨터와 대화할 때

- 대화 내용을 다른 사람이 볼 수 없도록 암호화
- 연결한 서버가 진짜인지 증명하는 역할
- 내가 허가받은 사용자라는 사실을 안전하게 증명하는 역할

<img width="580" alt="ssh-handshake" src="https://github.com/user-attachments/assets/6b0768c0-9f0d-417b-bac5-24d8d23a004d" />

이 모든 과정을 담당하는 것이 SSH다.

> 💡 GitHub에 코드를 올리거나, 리눅스 서버에 접속하거나, Supabase 같은 서비스를 사용할 때도 SSH가 활용된다.

## 왜 필요할까?
인터넷은 누구나 함께 사용하는 공용 네트워크다.

그래서 내 컴퓨터와 GitHub 서버가 통신할 때도 바로 연결되는 것이 아니라 여러 통신 장비를 거쳐 이동하게 된다.

<img width="480" alt="network-path" src="https://github.com/user-attachments/assets/c138bb9d-1f6c-4add-8833-3893dc2e6144" />

이 과정에서는 여러 가지 문제가 발생할 수 있다.
- 누군가 통신 내용을 훔쳐볼 수도 있다.
- 데이터를 중간에서 변조할 수도 있다.
- 사용자를 가짜 서버로 연결시킬 수도 있다.

예를 들어 사용자가 잘못된 주소로 접속하거나 중간에서 연결이 조작된다면,<br>
사용자는 GitHub에 접속했다고 생각하지만 실제로는 해커가 만든 서버와 통신하고 있을 수도 있다.

<img width="580" alt="fake-server" src="https://github.com/user-attachments/assets/683b6ff5-8d84-4a5a-9933-d05f3476dbba" />


인터넷에서는 상대방이 정말 내가 연결하려던 서버인지 확인하는 것도 생각보다 중요한 문제다.

## 무엇을 해결할까?
SSH는 이런 위험을 해결하기 위해 만들어졌으며 크게 세 가지를 해결한다.

- 통신 내용을 암호화한다.
- 연결한 서버가 진짜인지 확인한다.
- 사용자가 진짜인지 안전하게 증명한다.

> 즉, SSH는 안전하게 통신하기 위한 전체 규칙이라고 생각하면 된다.

## 사용자는 어떻게 인증할까?
SSH는 사용자를 인증하는 방법을 하나만 제공하는 것이 아니다.

대표적으로 다음과 같은 인증 방식을 지원한다.
- 비밀번호 인증(Password Authentication)
- 공개키 인증(Public Key Authentication)

SSH를 사용한다고 해서 반드시 SSH Key를 사용하는 것은 아니다.

예를 들어 일부 리눅스 서버는 지금도 SSH로 접속하면서 비밀번호를 입력해 로그인한다.

```
ssh hong@example.com

Password:
```

반면 GitHub는 **SSH로 접속할 때 비밀번호 인증을 지원하지 않고 공개키 인증만 사용**한다.

그래서 GitHub에 SSH로 연결하려면 먼저 SSH Key를 생성하고 공개키를 GitHub에 등록해야 한다.

> **💡 참고 사항**
>
> GitHub는 SSH 외에도 HTTPS 방식으로 저장소에 접근할 수 있다.<br>
> 다만 HTTPS에서는 비밀번호 대신 Personal Access Token(PAT) 을 사용하며, SSH와는 다른 인증 방식이다.
