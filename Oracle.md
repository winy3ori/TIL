Oracle은 Mac Os를 정식 지원 않으므로 설치를 위해서 별도 절차가 필요하다.
Mac OS에 Oralce DB를 설치하는 방법은 두 가지가 있다.

> Oracle Cloud에 DB를 띄워 사용하는 방법.
> 오픈소스 컨테이너 런타임 Colima를 사용해 oci-oracle-xe이미지를 x86/64가상 환경으로 띄워 사용하는 방법.

GitHub에 공유된 Nomad Coders 강의 소스코드를 clone한 뒤 npm i → npm start로 프로젝트를 실행했더니 다음과 같은 에러가 발생, 실행할 수 없었다.

$ npm start

...

node:internal/modules/cjs/loader:488
      throw e;
      ^

Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/tokenize' is not defined by "exports" in (프로젝트 경로)/node_modules/postcss-safe-parser/node_modules/postcss/package.json
    at new NodeError (node:internal/errors:371:5)
    at throwExportsNotFound (node:internal/modules/esm/resolve:429:9)
    at packageExportsResolve (node:internal/modules/esm/resolve:683:3)
	...
{
  code: 'ERR_PACKAGE_PATH_NOT_EXPORTED'
}

Node.js v18.2.0
원인
내 컴퓨터에 설치된 node 버전과 프로젝트에 설치된 패키지들의 버전이 충돌, Node가 잘못된 경로로 패키지를 import해서 발생하는 에러다.

내 경우 오래 전에 만들어져 업데이트되지 않은 프로젝트에서는 구버전 패키지를 사용하고 있어서 오류가 발생했다.

해결 방법
해결 방법은 두 가지가 있다. 아무거나 적용해서는 안 되고, 내 컴퓨터에 설치된 node 버전과 실행하려는 프로젝트의 상태에 따라 적합한 방법을 사용해야 한다.

내 컴퓨터에 설치된 node 버전이 사용하는 패키지에 비해 최신 버전일 경우 → node 버전을 LTS 버전으로 다운그레이드한다.(1) 컴퓨터에 설치된 노드 버전은 다음 명령으로 확인할 수 있다.
$ node -v
v18.2.0
프로젝트가 만들어진 지 오래 되었다.(오래된 구버전 패키지를 사용한다.) → 설치된 패키지를 업그레이드한다. (2) 프로젝트 패키지 버전 확인을 다음 명령으로 확인할 수 있다.
$ npm show 모듈명 version
내 프로젝트에서 사용중인 패키지들의 전체 버전을 확인할 때 npm-check-updates 패키지를 사용하면 편하다.
# npm-check-updates 라이브러리 전역에 설치
$ npm install -g npm-check-updates

# 최신버전 확인
$ ncu
1️⃣ node 버전 다운그레이드 — nvm 사용하기
node-version-manager(nvm) 패키지를 사용하면 시스템에 여러 개의 nodejs를 설치하고 사용할 버전을 전환할 수 있게 해준다.

nvm을 설치 및 사용하는 방법에 대해서는 이 글에서는 다루지 않는다. 이 블로그에서 잘 설명되어있다.

현재 node의 LTS 버전은 18.18.0, 가장 최신 버전은 20.8.0이다.(2023.10 기준)

만약 내 node 버전이 18.18.0 이상이거나, 프로젝트에서 사용하는 패키지가 오랫동안 node 버전에 맞춰 업데이트 되지 않았을 경우 node를 LTS 이하의 버전으로 다운그레이드가 필요할 수 있다.

단, 15 이하의 오래된 node 버전을 사용하면 앞으로 더 많은 외부 패키지를 사용해야 할 때 충돌이 있을 수도 있겠다.

