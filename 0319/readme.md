touch

sudo snap install tree
~ mkdir 0319
~ mkdir 0319/choi
~ mkdir 0319/choi/cs101
~ mkdir 0319/chang
~ mkdir 0319/chang/doc
~ mkdir 0319/chang/test
~ mkdir 0319/chang/test/cs1.txt
~ cd 0319 tree
     * = all
	? == one
	rm=제거시키는 것
ls/bin/??
ls/bin/*

0319/chang/test/cs1.txt의 이름을 cssw.txt로 변경하시오
0319/chang/test/cs2.txt 파일을 choi/cs101로 복사하시
	```
#### 코드블록 만드는 법 
코드블록은 밑에 이점 3개임 \`뒤에점 3개 
```

this_is_hwi@DESKTOP-O21OSOF:~/0319$ cd chang
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang$ mkdir doc
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang$ cd ..
this_is_hwi@DESKTOP-O21OSOF:~/0319$ tree
.
├── chang
│   ├── doc
│   └── test
│       └── cs1.txt
└── choi
    └── cs101

6 directories, 0 files
this_is_hwi@DESKTOP-O21OSOF:~/0319$ cd test
-bash: cd: test: No such file or directory
this_is_hwi@DESKTOP-O21OSOF:~/0319$ cd chang
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang$ cd test
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ mkdir cs2.txt
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ cd ..
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang$ cd ..
this_is_hwi@DESKTOP-O21OSOF:~/0319$ tree
.
├── chang
│   ├── doc
│   └── test
│       ├── cs1.txt
│       └── cs2.txt
└── choi
    └── cs101
```
```
this_is_hwi@DESKTOP-O21OSOF:~/0319$ cd chang/test
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ ls
cs2.txt  cssw.txt
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ mv ./cs2.txt choi/cs101
mv: cannot move './cs2.txt' to 'choi/cs101': No such file or directory
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ mv ./cs2.txt ../../choi
/cs101
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang/test$ cd ..
this_is_hwi@DESKTOP-O21OSOF:~/0319/chang$ cd ..
this_is_hwi@DESKTOP-O21OSOF:~/0319$ tree
.
├── chang
│   ├── doc
│   └── test
│       └── cssw.txt
└── choi
    └── cs101
        └── cs2.txt

7 directories, 0 files
this_is_hwi@DESKTOP-O21OSOF:~/0319$


```
## "A"=41h=65
## 'a'=61h=97
공백은 30h=48임 기본적인거
동기 비동기,블럭킹,난블럭킹


이해하고 요약하고 암기하고 표현하기 ㅡ공부ㅡ
우분투에서는 뭐가 실행되고 있을까
bash가 실행중이여야지 된다


$ ls –la /usr/bin/a*

ls: "list"의 줄임말로, 파일과 디렉토리를 나열하는 명령어
-la: 옵션으로, ls 명령어에 대한 추가적인 기능을 제공함
-l: 긴 형식(long format)으로 파일과 디렉토리의 정보
예시 파일의 소유자, 그룹, 크기, 생성일
-a: 숨겨진(hidden) 파일도 포함하여 모든 파일과 디렉토리를 나열
파일이나 디렉토리 이름이 .으로 시작하는 경우 숨겨진 파일로 간주
/usr/bin/a*: /usr/bin 디렉토리 내에서 이름이 a로 시작하는 모든 파일과 디렉토리를 나열



vi나가는 법 다하고 나서 esc누르고나서 
:누르고 wq라고 입력하면 저장되고 나옴

번외
 작업디렉토리(작업트리)
버전 관리의 대상이 위치하는 곳 거시적으로 확인가능
버전을 만들다는 특정순간의 변경 사항을 기억한다는 것
새로운 수정이 생기면 새로운 버전이 생긴다가 디폴트고
굳이 계속 새로운 버전을 만들필요는 없다만 인지하기
프로젝트가 위치할 공간을 이야기한다고 봄

![KakaoTalk_20240319_194736937](https://github.com/this-is-hwi/sysprogramming/assets/163086402/f1aeda94-49b8-420c-9efa-7df2434b6e69)
