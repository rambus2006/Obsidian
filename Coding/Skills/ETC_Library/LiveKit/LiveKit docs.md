#  개요
- Room  객체를 통해 Live Kit 서버에 연결한다.
- 화상통화처럼 여러 사람이 한 방(Room 객체)에 모여 실시간 오디오, 비디오, 데이터를 공유할 수 있습니다. 

# 설치하는 법 
- LiveKit에는 JavaScript, Swift, Android, React Native, Flutter, Unity를 포함한 모든 주요 플랫폼을 위한 오픈 소스 SDK가 포함되어 있습니다.
- javascript(npm or yarn)
```
npm install livekit-client @livekit/components-react @livekit/components-styles --save
```

# 설치 후 방 연결 
- Room 객체는 고유한 문자열로 된 이름으로 식별 가능 
- 방 자체는 첫번째 참여자가 참여하면 자동으로 생성되고, 마지막 참가자가 나가면 닫힘
> 1. 방에 연결할 때
- 참가자 ID 
	- weUrl : LiveKit 서버의 WebSocket URL
	- token: 각 참가자가 연결하기 위해 사용해야하는 토큰
		- 방 이름, 참가자의 신원,권한을 인코딩 
		- javascript
		```
		const room = new Room();
		await room.connect(wsUrl, token);
		```
		- React
```
<LiveKitRoom audio={true} video={true} token={token} serverUrl={wsUrl}>
	<!-- your components here -->
</LiveKitRoom>
```

> 2. 방 연결에 성공했을 때 
- 연결에 성공했을 때 Room 객체 내부에는 
	- localParticipant : 현재 사용자를 나타내는 객체 
	- remoteParticipants : 방에 있는 다른 참가자의 배열 
	
> 3. 연결에 해제할 때 
- `Room.disconnect()` 메서드를 호출 한 뒤 `disconnect()` 를 통해 연결을 해제할 수 있습니다. 
- 만약 `Room.disconnect()` 를 호출하지 않고 앱을 종료할 경우 참여자는 15초 후에 사라진다. 

# 연결 안정성 
- Live Kit 은 다양한 네트워크 환경에서 안정적인 연결을 지원한다. 
- WebRTC 연결 유형을 위에서 아래쪽으로 가며 시도한다. (만약 위에꺼가 안되면 아래쪽꺼로 점점 내려간다.)

1. UDP를 통한 ICE: 대부분의 조건에서 사용되는 이상적인 연결 유형
2. UDP(3478)를 사용한 TURN: ICE/UDP에 접근할 수 없을 때 사용됨
3. TCP를 통한 ICE: 네트워크가 UDP를 허용하지 않을 때 사용됨(예: VPN 또는 회사 방화벽을 통한)
4. TLS를 사용한 TURN: 방화벽이 아웃바운드 TLS 연결만 허용하는 경우 사용됨