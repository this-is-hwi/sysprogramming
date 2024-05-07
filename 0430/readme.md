i-node 보안쪽에 들어갈수도
분야마다 전부 달라진다
커널에 대한 이해
운영체제의 이해 커널에 운영체제의구현

파일은 i-node이용

부트 블록 컴퓨터를 시작하는 부팅
실질적인적 정보는 i-list에 있다
자료구조를 정하기전에 문제해결부터해야한
---.exe
---.com 이거 둘을 동시에 실행시키는게 
batch시스템이
사진1
![Pasted image 20240430172102](https://github.com/this-is-hwi/sysprogramming/assets/163086402/e1437a66-4698-40d8-8aed-bb2de7723743)


-파일 타입검사 함수

사진2

![Pasted image 20240430172046](https://github.com/this-is-hwi/sysprogramming/assets/163086402/44c32507-a4c7-4df0-a0d2-59cab61a6aeb)

폴더가 뭐냐? 윈도우에서 만들어진 용어
디렉토리 파일을 효율적으로 관리하는 시스템
디렉토리내에서 디렉토리가 들어갈수있음 서로 관련있는 파일들의 집합체

포맷을 하는 순간에 그운영체제가 사용할수있게 하ㄴ는것
그순간 루트디렉토리가된다 
즉 전부 트리구조로 나와있다 디렉토리안에는 디렉토리나 파일이들어있음
파일엔 아이노드가 있다
디렉토리도 파일처럼 처리한다
키보드도 모니터도 하나의 파일처럼 취급한다
전부 아이노드를 가지고있다

파일은 바이트의 연속이다

왜전부 8비트 64비트 이단위로 끊어서 보내냐?
그이유는 호환성때문이다
확장도 용이하고 나누면 8비트가 될수있기에 파일들간의 호환성을 위해서다.

ls시스템 구현하기

USAGE
LINK (옵션) F1 F2 이실행파일의 사용법은 이거이다
arg0 arg1 arg2 arg3
이걸로 if문 작성 가능 
arg1이뭐면 if 이런식으로 구현가

7장 실습 결과 사

![스크린샷 2024-04-30 182314](https://github.com/this-is-hwi/sysprogramming/assets/163086402/f2dd5976-772f-4696-85bb-fa39bebaf38b)

![스크린샷 2024-04-30 183449](https://github.com/this-is-hwi/sysprogramming/assets/163086402/d3cb6781-3f8e-4101-9414-4f8bdd6e0d72)


![스크린샷 2024-04-30 184150](https://github.com/this-is-hwi/sysprogramming/assets/163086402/4f4804c5-ea8e-4f29-b75a-42a26062e8c5)

![스크린샷 2024-05-02 165354](https://github.com/this-is-hwi/sysprogramming/assets/163086402/3890b0aa-01c6-44c0-a844-263cf9adc4a1)

![스크린샷 2024-05-02 165414](https://github.com/this-is-hwi/sysprogramming/assets/163086402/e18997ae-951b-4d29-b50a-18d99c3c4678)
rlink

![스크린샷 2024-05-02 165443](https://github.com/this-is-hwi/sysprogramming/assets/163086402/958ad5c9-38d8-4893-9ef3-774bdd62336c)
