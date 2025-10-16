
# 1. openvidu-library 링크 

- 튜토리얼: https://docs.openvidu.io/en/stable/tutorials/openvidu-library-react/
- 웹사이트: https://openvidu.io/

# 2. OpenVidu api 소개 
- 여기서는 3.40 버전)

> 1. **Docker Desktop을** 열고 오른쪽 하단에 있는 **"터미널"** 버튼을 클릭합니다 .

[도커 설치하는 방법 ](ProgramSettings/nvm(Node.js).md)
![[Pasted image 20251015154408.png]]

> 2. 다음 명령을 복사하여 터미널에 붙여넣으세요.

```
docker compose -p openvidu-meet -f oci://openvidu/local-meet:latest up -y openvidu-meet-init
```
![[Pasted image 20251015154456.png]]

> 3. 사이트 접속해서 방 만들어보기 
- 관리 사이트 http://localhost:9080
- 기본 사용자 ID,PW
	- 사용자 이름:`admin`
	- 비밀번호:`admin`
- RestAPI를 사용하여  OpenVidu Meet을 내장할 수 있다. 
- API 키:`meet-api-key`

> 4. HTML로 api 가져와보기 
- https://openvidu.io/3.4.0/meet/embedded/intro/
```
<openvidu-meet room-url="https://YOUR_DOMAIN/room/your-room?secret=1234567"></openvidu-meet>
```

- 대략적으로 이런 걸 할 수 있는 api라고 생각하면된다. 
---
# 3. 튜토리얼  
## { 1. 직접 연결(Direct Link) 실행하기  } 
- [원본 문서 바로가기](https://openvidu.io/3.4.0/meet/embedded/tutorials/direct-link/#connecting-this-tutorial-to-an-openvidu-meet-production-deployment)
> 1-1. 도커 연결 

```
docker compose -p openvidu-meet -f oci://openvidu/local-meet:3.4.0 up -y openvidu-meet-init
```

> 1-2. 튜토리얼 코드 다운로드 

```
git clone https://github.com/OpenVidu/openvidu-meet-tutorials.git -b 3.4.0
```

> 1-3. 애플리케이션 실행 
- 명령어 실행 
```
cd openvidu-meet-tutorials/meet-direct-link
npm install
npm start
```
- 웹사이트 실행 [`http://localhost:6080`](http://localhost:6080/).
> 1-4. 결과 화면
- 대충 이런 화면이 보인다. 
![[Pasted image 20251015161329.png]]

