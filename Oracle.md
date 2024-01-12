Mac OS에서 Oracle DB 사용을 위해 필요한 절차

### Colima 설치
> 💡 Colima는 무거운 Docker Desktop을 대신해 간단한 CLI 환경에서 도커 컨테이너들을 실행할 수 있는 오픈 소스 S/W

```
brew install colima
```
<br><br>
### Docker 설치

Docker 홈페이지에서 Docker Desktop 설치
만약 Docker Engine만 설치하고 싶은 경우 brew로 도커 엔진만 설치 가능

```
brew install docker
```
<br><br>
### Colima 실행
colima를 x86_64 환경으로 띄워준다.
```
colima start --memory 4 --arch x86_64
```

`docker ps` 명령어를 사용해 작동 확인
<br><br>
### Docker 컨테이너 실행
```
docker run --restart unless-stopped --name oracle -e ORACLE_PASSWORD=pass -p 1521:1521 -d gvenzl/oracle-xe
```

- --restart 옵션에서 `unless-stopped` 설정시 재부팅시 자동으로 Oracle DB 실행
- -- name 옵션에서 이름 설정시 컨테이너 ID 대신 편한 이름 사용 가능
<br>

`docker ps` 로 Oracle 컨테이너가 떠있는 상태 확인

```
docker logs -f oracle (컨테이너명)
```
`docker logs` 로 로그 확인시 "DATABASES IS READY TO USE!" 가 뜨면 성공


`control(^) + c` 로 종료
<br><br>
### SQL Plus 실행
```
docker exec -it 컨테이너 이름 sqlplus
```
user-name : system 
password : 설정값

