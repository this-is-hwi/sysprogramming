```
파일 및 레코드 잠금 원리
어떻게 프로세스 사이에 데이터를 주고받을 수 있을까?
 한 프로세스가 파일에 쓴 내용을 다른 프로세스가 읽음
 문제점
 한 프로세스가 파일 내용을 수정하는 동안에 다른 프로세스가 그 파일을 읽는 경우
 두 개의 프로세스가 하나의 파일에 동시에 접근하여 데이터를 쓰는 경우
```
###잠금
```
파일 혹은 레코드(파일의 일부 영역) 잠금
한 프로세스가 그 영역을 읽거나 수정할 때 다른 프로세스의 접근을 제한
 잠금된 영역에 한 번에 하나의 프로세스만 접근
특히 레코드에 쓰기(혹은 수정)를 할 경우 대상 레코드에 대해 잠금을 해서 다른
프로세스가 접근하지 못하게 해야 한다.
```
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/12ac0000-2219-44e6-abfd-8a82e35884b3)

```
구현
fcntl( ) 함수
파일 및 레코드 잠금을 구현할 수 있다.
잠금의 종류
F_RDLCK : 여러 프로세스가 공유 가능한 읽기 잠금
F_WRLCK : 한 프로세스만 가질 수 있는 배타적인 쓰기 잠금
 fd는 대상이 되는 파일 디스크립터
cmd
F_GETLK : 잠금 검사
F_SETLK : 잠금 설정 혹은 해제
F_SETLKW: 잠금 설정(블로킹 버전) 혹은 해제
flock 구조체
잠금 종류, 프로세스 ID, 잠금 위치 등

```
```c
#include <sys/types.h>
#include <unistd.h>
#include <fcntl.h>
int fcntl(int fd, int cmd, struct flock *lock);
cmd에 따라 잠금 검사 혹은 잠금 설정을 한다. 성공하면 0 실패하면 -1을 리턴
```
```
잠금함수
F_LOCK : 지정된 영역에 대해 잠금을 설정한다.
이미 잠금이 설정되어 있으면 잠금이 해제될 때까지 기다린다.
F_TLOCK : 지정된 영역에 대해 잠금을 설정한다.
이미 잠금이 설정되어 있으면 기다리지 않고 오류(-1)를 반환한다.
F_TEST : 지정된 영역이 잠금되어 있는지 검사한다. 잠금이 설정되어 있지 않으면
0을 반환하고 잠금이 설정되어 있으면 –1을 반환한다.
F_ULOCK : 지정된 영역의 잠금을 해제한다.

```

##시스템 호출
```
 시스템 호출은 커널에 서비스 요청을 위한 프로그래밍 인터페이스
응용 프로그램은 시스템 호출을 통해서 커널에 서비스를 요청한다
```

```파일
C 프로그램에서 파일은 왜 필요할까?
변수에 저장된 정보들은 실행이 끝나면 모두 사라진다.
정보를 영속적으로 저장하기 위해서는 파일에 저장해야 한다.
유닉스 파일
모든 데이터를 연속된 바이트 형태로 저장한다

텍스트 파일(text file)
사람들이 읽을 수 있는 문자들을 저장하고 있는 파일
텍스트 파일에서 “한 줄의 끝”을 나타내는 표현은 파일이 읽어 들여질 때, C 내부의
방식으로 변환된다.
이진 파일(binary file)
모든 데이터는 있는 그대로 바이트의 연속으로 저장
이진 파일을 이용하여 메모리에 저장된 변수 값 형태 그대로 파일에 저장할 수 있다
```
```파일 열기
파일을 사용하기 위해서는
반드시 먼저 파일 열기(fopen)를 해야 한다.
파일 열기를 하면 FILE 구조체에 대한 포인터가 리턴되며
FILE 포인터는 열린 파일을 나타낸다.
함수 fopen()
FILE *fopen(const char *filename, const char *mode);
const char *filename: 파일명에 대한 포인터
const char *mode: 모드로 파일을 여는 형식
```
```c
FILE *fp;
fp = fopen(“~/sp/text.txt", "r");
if (fp == NULL) {
printf("파일 열기 오류\n");
}
fp = fopen("outdata.txt", "w");
fp = fopen("outdata.txt", "a"); 

```
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/8e9ee8f5-f0c5-4c90-8573-005694a5a55c)

```구조체
파일 관련 시스템 호출
파일 디스크립터 (file descriptor)
C 표준 입출력 함수
fopen( ) 함수로 파일을 열면 FILE 포인터(FILE *)가 리턴됨
열린 파일을 가리키는 FILE 구조체에 대한 포인터
FILE 포인터를 표준 입출력 함수들의 인수로 전달해야 함
#include <stdio.h>
FILE 구조체
하나의 스트림에 대한 정보를 포함하는 구조체
버퍼에 대한 포인터, 버퍼 크기 …
파일 디스크립터

구조체란 FILE 구조체: 열린 파일의 현재 상태를 나타내는 필드 변수들
특히 파일 입출력에 사용되는 버퍼 관련 변수들
```
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/0bfcb226-f93c-4d25-bbf7-1569b5a7cb52)

```파일내위치
현재 파일 위치(current file position)
열린 파일에서 다음 읽거나 기록할 파일 내 위치
파일 위치 포인터(file position pointer)
시스템 내에 그 파일의 현재 파일 위치를 저장하고 있다.
```
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/e52d442c-f8b9-4eac-a924-6c4477bae317)

```
파일 위치 이동
fseek(fd, 0L, SEEK_SET); 파일 시작으로 이동(rewind)
fseek(fd, 100L, SEEK_SET); 파일 시작에서 100바이트 위치로
fseek(fd, 0L, SEEK_END); 파일 끝으로 이동(append)
레코드 단위로 이동
fseek(fd, n * sizeof(record), SEEK_SET); n+1번째 레코드 시작위치로
fseek(fd, sizeof(record), SEEK_CUR); 다음 레코드 시작위치로
fseek(fd, -sizeof(record), SEEK_CUR); 전 레코드 시작위치로
파일끝 이후로 이동
fseek(fd, sizeof(record), SEEK_END); 파일끝에서 한 레코드 다음
위치로 이동
```

```c라이브러리버퍼
C 라이브러리 버퍼 사용 목적
 디스크 I/O 수행의 최소화
• read (), write () 함수 호출의 최소화
최적의 크기 단위로 I/O 수행
시스템 성능 향상
C 라이브러리 버퍼 방식
완전 버퍼(fully buffered) 방식
-버퍼가 꽉 찼을 때 실제 I/O 수행
디스크 파일 입출력

줄 버퍼(line buffered) 방식
-줄 바꿈 문자(newline)에서 실제 I/O 수행
터미널 입출력 (stdin, stdout)
버퍼 미사용(unbuffered) 방식
-버퍼를 사용하지 않는다.
표준 에러 (stderr)
```
```
파일은 모든 데이터를 연속된 바이트 형태로 저장한다.
파일을 사용하기 위해서는 반드시 파일 열기 fopen()를 먼저 해야 하며 파일 열기를 하면
FILE 구조체에 대한 포인터가 리턴된다.
FILE 포인터는 열린 파일을 나타낸다.
fgetc() 함수와 fputc() 함수를 사용하여 파일에 문자 단위 입출력을 할 수 있다.
fgets() 함수와 fputs() 함수를 이용하여 텍스트 파일에서 한 줄씩 읽거나 쓸 수 있다.
fread()와 fwrite() 함수는 한 번에 일정한 크기의 데이터를 파일에 읽거나 쓴다.
열린 파일에서 다음 읽거나 쓸 파일 내 위치를 현재 파일 위치라고 하며 파일 위치 포인터가
그 파일의 현재 파일 위치를 가리키고 있다.
fseek() 함수는 현재 파일 위치를 지정한 위치로 이동시킨다. 
```
###scanf
```
scanf 함수의 기본 개념
scanf 함수는 표준 입력(일반적으로 키보드)으로부터 데이터를 읽어 지정된 형식으로 변환하고, 해당 데이터를 변수에 저장합니다. scanf 함수의 기본적인 형식은 다음과 같습니다:

c
코드 복사
int scanf(const char *format, ...);
format: 형식 문자열로, 읽어들일 데이터의 형식을 지정합니다.
...: 형식 문자열에 따라 데이터를 저장할 변수의 주소를 나열합니다.리눅스에서 scanf의 동작
리눅스 시스템에서 scanf는 표준 입력을 사용하여 데이터를 읽어들입니다. 이는 주로 터미널 입력을 의미합니다. scanf는 입력 버퍼에서 데이터를 읽어와 형식 문자열에 맞게 변환합니다.

입력 버퍼와 scanf의 동작:

입력 버퍼: 사용자가 터미널에 입력한 데이터는 먼저 입력 버퍼에 저장됩니다.
형식 지정자 처리: scanf는 형식 문자열에 따라 입력 버퍼에서 데이터를 읽어오고, 지정된 형식으로 변환하여 변수에 저장합니다.
공백 문자 처리: scanf는 공백 문자(공백, 탭, 줄 바꿈)를 무시하고, 다음 유효한 입력을 기다립니다.
```

```c
#include <stdio.h>

int main()
{
    int numinput;
    char charinput;
    scanf("%d", &numinput);
    printf("%d\n", numinput);
    scanf(" %c", &charinput);
    printf("%c\n", charinput);
    return 0;
}
```
