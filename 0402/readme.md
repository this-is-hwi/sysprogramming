# 04/02
long.c를 main.c, copy.c, copy.h로 변환 시킴
gcc컴파일러로 컴파일가능

디렉토리하나당 Makefile 1개만 만들 수 있다.

단일 모듈 프로그램
```코드의 재사용(reuse)이 어렵고,
여러 사람이 참여하는 프로그래밍이 어렵다
예를 들어 다른 프로그램에서 copy 함수를 재사용하기 힘들다
```
다중 모듈 프로그램
```여러 개의 .c 파일들로 이루어진 프로그램
일반적으로 복잡하며 대단위 프로그램인 경우에 적합
```
### make sys
```make 시스템

대규모 프로그램의 경우에는 헤더, 소스 파일, 목적 파일, 실행 파일의 모든 관 계를 기억하고 체계적으로 관리하는 것이 필요
make 시스템을 이용하여 효과적으로 작업

Makefile 

실행 파일을 만들기 위해 필요한 파일들과 만드는 방법을 기술  make 시스템은 파일의 상호 의존 관계를 파악하여 실행 파일을 쉽게 다시 만듬 

$make [-f 메이크파일]
옵션이 없으면 Makefile 혹은 makefile을 사용
```
리눅스는 모든 디바이스및 모든것을 다 파일로 인식함 즉 open해야지만 사용가능

### 유닉스에서 파일
	연속된 바이트의 나열
	특별한 다른 포맷을 정하지 않음
	디스크 파일뿐만 아니라 외부 장치에 대한 인터페이스
open하고 use하고 close는 무조건 해야한다.
### open()
```flag  O_RDONLY
읽기 모드
read()
호출은 사용 가능 
O_WRONLY 
쓰기 모드, write() 
호출은 사용 가능 
O_RDWR 
읽기/쓰기 모드, read(), write() 호출 사용 가능 
O_APPEND 
데이터를 쓰면 파일끝에 첨부된다. 
O_CREAT 
해당 파일이 없는 경우에 생성하며 mode는 생성할 파일의 사용권한을 나타낸다.
```
### 파일오픈 오류
make fopentest만들었때

```
cc     fopentest.c   -o fopentest
fopentest.c: In function ‘main’:
fopentest.c:12:17: warning: implicit declaration of function ‘close’; did you mean ‘pclose’? [-Wimplicit-function-declaration]
   12 |                 close(fd);
      |                 ^~~~~
      |                 pclose
fopentest.c:13:9: warning: implicit declaration of function ‘exit’ [-Wimplicit-function-declaration]
   13 |         exit(0);
      |         ^~~~
fopentest.c:5:1: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
    4 | #include <fcntl.h>
  +++ |+#include <stdlib.h>
    5 | int main(int argc, char *argv[])
fopentest.c:13:9: warning: incompatible implicit declaration of built-in function ‘exit’ [-Wbuiltin-declaration-mismatch]
   13 |         exit(0);
      |         ^~~~
fopentest.c:13:9: note: include ‘<stdlib.h>’ or provide a declaration of ‘exit’
```

리턴은 자기를 호출한 곳으로 돌아온다 
리턴은 바로메인으로 돌아간다
exit는 전체를 종료해버린다
운영체제에게 돌아간다. 나 끝낼께 말하는 것은 exit임
fwd 명령어 구현하세요가 학기말 레포트가 됌
ls명령어구현가능

!=제일 최근에 실행한것
data type이 있어야지 변수를 만들수있다.
c언어의 datatype 

ssize_t unsigned랑 같다 32비트 64비트데이터에서 서로 달라진다
-1을 리턴하기때문에 
전부다 값만 들어감 배열 
버퍼의 단위는 뭘까? 바이트다 
파일 디스크립터는
파이프 피포 소켓 터미널 디바이스 일반파일등 종류에 상관없이 모든 열려있는 파일를 참조한다
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/11e8510b-8a2b-46d8-856a-cdc76cd2ae2c)

