----
####  ps : 디렉터리 이하에 프로세스와 연관된 가상 파일시스템의 내용을 토대로 프로세스 정보를 출력한다.

 * 기본프로세스 출력
 
 a : 터미널과 연관된 프로세스만 출력
 
 x : 터미널과 연관되지 않는 프로세스만 출력
 
 -A : 모든 프로세스 출력(-e와 동일하다.)
 
 -a : 세션 리더와 커미널과 연관된지 않은 프로세스를 제외하고 모든 프로세스를 출력
  
* 지정한 프로세스 출력

p : 지정한 PID 목록의 정보만 출력

-C : 지정한 프로세스의 실행 파일 이름의 정보만 출력

-u : 특정 사용자의 프로세스 정보를 출력

* 프로세스 표시 형식

u : 프로세스의 소유자 정보를 함께 출력

l : BSD 형식의 긴 형식으로 출력

e : 프로세스 정보와 함께 프로세스의 환경변수 정보도 출력

-l : 긴 포맷으로 출력

-o : 사용자 정의 형식 지정 가능

* 프로세스 표시 형식

f : 프로세스 계층을 텍스트 형식의 트리구조를 보여줌.

-f : 전체 포맷으로 출력

----
####  top : 시스템에서 현재 실행중인 프로세스에 대한 정보를 실시간으로 제공한다.
|옵션|의미|
|----|----|
|-n |지정한 숫자만큼 화면 출력을 갱신한후 명|
|-u |지정한 사용자의 프로세스를 모니터링|
|-b |출력결과를 파일이나 다른 프로그램으로 전달|
|-d |화면갱신주기를 초 단위로 설정|
|-p |지정한 PID 프로세스를 모니터링|

![openSW  ](https://user-images.githubusercontent.com/83820089/172012422-ed9869e4-893a-4caf-a9f3-19bd5c3fbc86.png)


----

#### kill : 불필요한 프로세스, 잘못 실행된 프로세스를 죽이는데 사용된다.
* 시그널은 프로세스 사이의 통신 수단인데 어떤 프로세스에 메세지를 보내 프로세스를 제어한다. 명령어를 실행함으로써 프로세스가 시작되고 그 프로세스를 제어하기 위하여 사전에 정의된 시그널이 존재한다.

|번호|시그널|의미
|----|-----|----|
|1|SIGHUP| 터미널에서 접속이 끊겼을때 보내지는 시그널, 변화된 내용을 적용하기 위해 재시작 할 때 사용된다.|
|2|SIGINT| 인터럽트 시그널로 실행을 중지시킴, CtrL+c 입력시 보내지는 시그널|
|3|SIGQUIT| 실행 중지 시그널로서 CtrL+\ 입력시 보내지는 시그널|
|4|SIGKILL| 프로세스를 강제로 종료 시키는 시그널|
|5|SIGTERM| kill의 기본 시그널로 정상 종료 시키는 시그널|
|6|SIGCONT| 시그널에 의해 정지된 프로세스를 다시 실행시키는 시그널|
|7|SIGSTOP| 정지 시그널|
|8|SIGTSTP| 일시정지 시키는 시그널로서 Ctrl+Z 입력시 보내지는 시그널|

-----

#### jobs : 작업이 중지된 상태, 백그라운드로 진행 중인 작업 상태, 변경 되었지만 보고 되지 않은 상태등을 표시하는 명령어이다.  현재 돌아가고 있는 백그라운드 프로세스 리스트를 모두 출력해준다. 

* 백그라운드 프로세스는 스택처럼 쌓이는데, +는 스택의 가장위, -는 바로 그 다음 밑에 있다는 뜻이다.

![opensw2](https://user-images.githubusercontent.com/83820089/172012550-96e73f91-14c9-49f7-a38f-860fbd5efb0a.png)

|옵션|설명|
|----|----|
|-l|프로세스 그룹 ID를 state 필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|

-----

### vim 에디터에서 매크로 사용법

* 매크로 기록 (q)

vim의 중립 모드에서 q를 누른 다음 매크로 이름으로 사용할 알파벳을 눌러준다. 

예를 들어 qa라고 한다면 a라는 매크로를 기록하기 시작한다. 

매크로를 기록하면서 맨 밑에 --recording--이라고 뜰 것이며 기록이 끝났으면 다시 중립모드에서 q를 눌러준다.

* 매크로 재생 (@)

 중립모드에서 @a 를 누르면 저장했던 매크로 a가 재생된다. 

 10@a 라고 한다면 매크로 a가 10회 실행이 된다.

 @@를 누르면 제일 마지막에 재생된 매크로, 가장 최근에 재생한 매크로가 재실행된다.
 
----

#### 코드 넣어보기

````c
#include<stdio.h>
#include<string.h>
int ch10_main(void) {
    char text[50], key[10], cipherText[50], plainText[50] = " ";
    
    gets(text);
    
    scanf("%s", key);

    int length = strlen(key);
    printf("암호문(16진수) = ");
  
    for (int i = 0; i < strlen(text); i++) {
        cipherText[i] = text[i] ^ key[i % length];
        plainText[i] = cipherText[i] ^ key[i % length];
        printf("%x", cipherText[i]);
    }
  
    printf("\n");
    printf("복호문 = %s", plainText);
    return 0;
}


