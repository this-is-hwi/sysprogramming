```
fork ()
 부모 프로세스를 똑같이 복제하여 새로운 자식 프로세스를 생성
자기복제(自己複製)

 fork()는 한 번 호출되면 두 번 리턴한다.
자식 프로세스에게는 0을 리턴하고
부모 프로세스에게는 자식 프로세스 ID를 리턴한다.
부모 프로세스와 자식 프로세스는 병행적으로 각각 실행을 계속한다

이후의 파일 공유는?
자식은 부모의 fd 테이블을 복사한다.
부모와 자식이 같은 파일 디스크립터를 공유
같은 파일 오프셋을 공유
부모와 자식으로부터 출력이 서로 섞이게 됨
자식에게 상속되지 않는 성질
fork()의 반환값
프로세스 ID
파일 잠금
설정된 알람과 시그널
```

``` c
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);
새로운 자식 프로세스를 생성한다. 자식 프로세스에게는 0을 리턴
하고 부모 프로세스에게는 자식 프로세스 ID를 리턴한다.
```

```wait()
자식 프로세스 중의 하나가 끝날 때까지 기다린다.
끝난 자식 프로세스의 종료 코드가 status에 저장되며
끝난 자식 프로세스의 번호를 리턴한다
```

```exec()
프로세스가 exec() 호출을 하면,
그 프로세스 내의 프로그램은 완전히 새로운 프로그램으로 대치
자기대치(自己代置)
새 프로그램의 main()부터 실행이 시작된다.
```

###추가로 알아본 바
```
1. fork()
fork() 시스템 호출은 현재 프로세스(부모 프로세스)를 복사하여 새로운 프로세스(자식 프로세스)를 생성합니다. 이때 자식 프로세스는 부모 프로세스의 거의 모든 속성을 복사하지만, 몇 가지 차이점이 있습니다.

시스템 호출: fork()
리턴 값:
부모 프로세스에서는 자식 프로세스의 PID가 반환됩니다.
자식 프로세스에서는 0이 반환됩니다.
```
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();
    
    if (pid == -1) {
        perror("fork failed");
        return 1;
    }
    
    if (pid == 0) {
        // 자식 프로세스
        printf("This is the child process\n");
    } else {
        // 부모 프로세스
        printf("This is the parent process with child PID: %d\n", pid);
    }
    
    return 0;
}
```

```
2. exec()
exec() 계열 함수는 현재 프로세스를 새로운 프로그램으로 교체합니다. fork()와 함께 사용되는 경우가 많습니다. exec()는 실행하려는 프로그램을 지정된 경로에서 찾고, 해당 프로그램으로 현재 프로세스를 대체합니다.

시스템 호출: execl(), execle(), execlp(), execv(), execve(), execvp()
리턴 값: 성공 시 리턴 값이 없고, 실패 시 -1이 반환됩니다.
```

```wait()
wait() 시스템 호출은 부모 프로세스가 자식 프로세스가 종료될 때까지 기다리도록 합니다. 자식 프로세스가 종료되면 자식 프로세스의 종료 상태를 수집합니다.

시스템 호출: wait(), waitpid()
리턴 값: 종료된 자식 프로세스의 PID, 실패 시 -1
```