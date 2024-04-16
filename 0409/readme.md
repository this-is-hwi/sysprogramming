void *

void포인터는 자료형이 무엇이든 간에 주소값만 바라봅니다.

1.char
1Byte를 의미
문자 저장(256개의 값 표현 가능)
2.short
2Byte임
작은 정수 저장에 사용
표현 범위: -32768 ~ 32767
3.int
4Byte임
정수 저장
표현 범위: -2,147,483,648 ~ 2,147,483,647
4.long
32bit 시스템 → 4Byte
64bit 시스템 → 8Byte
int 보다 더 큰 정수 값 저장에 사용
5.float
4Byte임
실수 저장
부동 소수점 표현 사용
6.double
8Byte
float 보다 더 정밀한 부동 소수점 저장에 사용

bit < nibble < byte < word < field < record < table < DB

ADT(추상 자료형)
ADT는 Abstract Data Type의 약자로, 우리말로 "추상 자료형"이라고 칭
자료형을 구현하기 이전, 이론적으로 이 자료형이 어떠한 구조로 생겼는지
이 자료형을 운용하기 위해 어떤 메소드를 만들어서 사용할 수 있는지 등등
실제 언어에 기본적으로 구현되어있는 primitive data type(원시 자료형) 이외에
자료형에 대한 이론 개념이라고 이해하면 된다
Stack, Queue, Deque, Heap 등이 해당한다
언어에 따라 원시 자료형이외에 선언되어 있는 경우도 있다.

![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/405a7fbe-2d97-4701-ada0-e9d4b3e44f55)
![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/f41582b0-7ef3-4236-81c8-42cbf816b7dc)
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include "student.h"

/* 학번을 입력받아 해당 학생의 레코드를 파일에서 읽어 출력 */
int main(int argc, char *argv[])  // argc: 인자 수, argv: 인자 값
{
    int fd, id;
    char c;
    struct student record;

    if (argc < 2)  // 인자 값이 부족한 경우
    {
        fprintf(stderr, "사용법 : %s 파일명\n", argv[0]);  // 표준 에러 스트림에 사용법 출력
        exit(1);  // 오류 코드 1과 함께 프로그램 종료
    }
    /* 파일 열기 */
    if ((fd = open(argv[1], O_RDONLY)) == -1)  // 해당되는 파일을 읽기 모드로 열기
    {
        perror(argv[1]);  // 파일 열기 실패 -> 오류 메시지 출력
        exit(2);  // 오류 코드 2와 함께 프로그램 종료
    }
    /* 학번 입력으로 학생 정보 검색 */
    do  // Y를 입력하는 동안 계속 반복
    {
        printf("\n검색할 학생의 학번 입력:");
        if (scanf("%d", &id) == 1)  // 정수형의 학번 입력 받기
        {
            lseek(fd, (id - START_ID) * sizeof(record), SEEK_SET);  // 파일 내 해당 학번으로 포인터 이동
            if ((read(fd, (char *)&record, sizeof(record)) > 0) && (record.id != 0))  // 해당 학번의 학생 정보가 유효한지 확인
                printf("이름:%s\t 학번:%d\t 점수:%d\n", record.name, record.id, record.score);  // 학생 정보 출력
            else
                printf("레코드 %d 없음\n", id);  // 리코드가 존재하지 않는 경우
        }
        else
            printf("입력 오류");  // 입력이 잘못된 경우
        printf("계속하겠습니까?(Y/N)");
        scanf(" %c", &c);  // 사용자 입력 받기
    } while (c == 'Y' || c == 'y');  // 사용자의 응답 받아 반복 여부 결정

    close(fd);  // 파일 디스크립터 닫기
    exit(0);    // 프로그램 정상 종료
}
```
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include "student.h"

/* 학번을 입력받아 해당 학생 레코드를 수정 */
int main(int argc, char *argv[]) // 인자 받기
{
    int fd, id;
    char c;
    struct student record;

    /* 인자값 검사 */
    if (argc < 2)
    {
        fprintf(stderr, "사용법 : %s 파일명\n", argv[0]);
        exit(1);
    }
    /* 파일 열기 */
    if ((fd = open(argv[1], O_RDWR)) == -1)  // 읽기 및 쓰기 모드로 파일 열기
    {
        perror(argv[1]);  // 파일 열기 실패한 경우 오류 메시지 출력
        exit(2);  // 오류 코드 2와 함께 프로그램 종료
    }
    /* 학번 입력 및 레코드 수정하기 */
    do  // Y를 입력하는 동안 계속 반복
    {
        printf("수정할 학생의 학번 입력: ");  
        if (scanf("%d", &id) == 1)  // 수정할 학생의 학번 입력 받기
        {
            lseek(fd, (long)(id - START_ID) * sizeof(record), SEEK_SET);  // 파일에서 해당 학번의 위치로 포인터 이동
            if ((read(fd, (char *)&record, sizeof(record)) > 0) && (record.id != 0))  // 학생 정보에서 해당 학번이 유효한지 확인
            {
                printf("학번:%8d\t 이름:%4s\t 점수:%4d\n", record.id, record.name, record.score);  // 수정 전 학생 정보 출력
                printf("새로운 점수: ");  // 새로운 점수 입력 받기
                scanf("%d", &record.score);
                lseek(fd, (long)-sizeof(record), SEEK_CUR);  // 현재 파일 포인터 위치에서 레코드 크기만큼 역방향으로 이동
                write(fd, (char *)&record, sizeof(record));  // 수정된 레코드를 파일에 기록
            }
            else  // 학번에 해당하는 레코드가 없는 경우
                printf("레코드 %d 없음\n", id);
        }
        else  // 입력 오류
            printf("입력오류\n");
        printf("계속하겠습니까?(Y/N)");
        scanf(" %c", &c);
    } while (c == 'Y' || c == 'y');  // 사용자의 응답 받아 반복 여부 결정

    close(fd);  // 파일 디스크립터 닫기
    exit(0);    // 프로그램 정상 종료
}
```


![image](https://github.com/this-is-hwi/sysprogramming/assets/163086402/ca05c9b1-59f6-4ade-a99c-d6b6d17b44f2)
