```
세미콜론을 이용해 명령어를 연속으로 처리하기
date; who
date 실행 후 who가 실행됨
date: 현재 시스템의 날짜와 시간이 기본 형식으로 출력
; (세미콜론)이 두 명령어를 순차적으로 실행되도록 함
who: 현재 시스템에 로그인한 모든 사용자의 정보를 출력

```
```
#!/bin/bash (Shebang)
유닉스 계열 운영 체제에서 스크립트 파일의 첫 번째 줄에 사용하는 특별한 형태의 주석
스크립트를 실행할 때 사용할 인터프리터(해석기)를 지정하는 역할
/bin/bash(절대 경로)에 위치한 bash 인터프린터를 사용해 스크립트를 실행함
스크립트 파일 생성 및 실행 방법
Vim을 이용한 파일 생성 및 저장
① 파일 생성
vi test1
② 작성
i 키를 눌러 입력 모드 진입
내용 작성
③ 저장 및 종료
입력 모드에서 Esc키를 눌러 명령 모드 실행
저장 및 종료하기
:wq!(저장 및 종료) 콜론 명령어 실행
또는 Shift + ZZ
```
```
스크립트 파일 생성 및 실행 자동화
스크립트를 생성하고, 실행 권한을 부여한 후, 해당 스크립트를 실행하는 일련의 단계를 자동화함
vi $1
chmod +x $1
./$1
① vi $i
스크립트를 실행할 때 사용자가 입력한 첫 번재 인자를 이용해 vi 편집기로 파일을 생성함
사용자가 실행된 Vim 에디터에서 스크립트 코드를 작성 하고, 저장 및 종료함
② chmod +x $1
생성한 파일에 실행 권한을 부여함
③ ./$1
생성된 파일을 실행함
실행
ex) test5 스크립트를 생성 및 실행하기

./run test5
```
```
test0 - 인자값 전달하기
현재 스크립트의 이름과 첫 번째, 두 번째, 세 번째 인자가 출력되는 스크립트
코드
echo $0 $1 $2 $3
$0: 현재 실행 중인 스크립트의 이름
$1, $2, ... : 스크립트에 전달된 첫 번째 인자, 두 번째 인자, ...
실행
./test0 arg1 arg2 arg3
```
```
test1 - 메시지 표시하기
#!/bin/bash
# This script displays the date and who's logged on
echo The time and date are:
date
echo "Let's see who's logged into the system:"
who
```
```
환경변수
#!/bin/bash
# display user information from the system.
echo "User info for userid: $USER"
echo UID: $UID
echo HOME: $HOME
```
```
사용자변수
#!/bin/bash
# testing variables
days=10
guest="Katie"
echo "$guest checked in $days days ago"
days=5
guest="Jessica"
echo "$guest checked in $days days ago"
```
```
변수할당
#!/bin/bash
# assigning a variable value to another variable
value1=10
value2=$value1
echo The resulting value is $value2
```
```
백틱
#!/bin/bash
# using the backtick character
testing=`date`
echo "The date and time are: " $testing
```
```
expr
#!/bin/bash
# An example of using the expr command
var1=10
var2=20
var3=`expr $var2 / $var1`
echo The result is $var3
```
```
[$operation]
var1=100
var2=50
var3=45
var4=$[$var1 * ($var2 - $var3)]
echo The final result is $var4
```
```
bash
#!/bin/bash
var1=100
var2=45
var3=$[$var1 / $var2]
echo The final result is $var3
```
