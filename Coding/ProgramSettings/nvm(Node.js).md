
# nvm
openvidu 라이브러리 튜토리얼을 따라하다가 node 버전 충돌 오류가 나서 nvm을 통해 node.js 버전 관리를 해야겠다고 생각했다. 

# nvm 설치하는 방법 

> 파일 설치 

1. 해당 링크로 들어간 뒤 nvm-setup.exe를 클릭해 설치한다. 
https://github.com/coreybutler/nvm-windows/releases

2. next 다 해준다. 
![](https://velog.velcdn.com/images/rambus/post/df2aed80-48fb-440a-810b-2f0d5298c18b/image.png)

3. window powershell 관리자 권한으로 실행 후 명령어 입력 
  ```
  setx PATH "$($env:PATH);C:\Program Files\nvm;C:\Program Files\nodejs"
  ```

4. 이후 nvm을 사용하여 원하는 버전을 cmd 에 입력하여 설치해주면 된다. 
```
//18버전 설치 
nvm install 18.18.0
```

> nvm 버전 명령어 

- 버전 확인 목록 
`nvm ls` 또는 `nvm list`
- 사용할 노드 버전 설정하기 
`nvm use 사용할 노드버전`
- 현재 사용하고 있는 노드 버전 확인 
`nvm current`

