Oracle은 Mac Os를 정식 지원 않으므로 설치를 위해서 별도 절차가 필요하다.  
Mac OS에 Oralce DB를 설치하는 방법은 두 가지가 있다.

> + Oracle Cloud에 DB를 띄워 사용하는 방법  
> + 오픈소스 컨테이너 런타임 Colima를 사용해 oci-oracle-xe이미지를 x86/64가상 환경으로 띄워 사용하는 방법

해당 포스트는 Docker x Colima 이용법에 대해 설명한다.

1. 먼저 brew를 이용해 Colima를 설치해준다.  
``` brew install colima ```
