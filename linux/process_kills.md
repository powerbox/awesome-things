# pkill
 
pkill과 kill의 차이점은 없다고 보셔도 무방합니다.
pkill은 kill명령어에서 ps명령어로 PID를 찾은 뒤 입력해야 되는 불편함을 개선한 것인데요.
솔직히 저는 차이를 못느끼겠네요.

## 정의
지정된 명령이 실행중인 특정 프로세스에 시그널을 보내는 겁니다.
이 때, 시그널을 입력하지 않으면 디폴트로 15번 시그널(정상작업종료)이 보내집니다.

``` 
Command#
root@localhost#pkill [-Signal] [프로세스명1] [프로세스명2] .......
 
ex)
root@localhost#pkill -9 httpd   // httpd 데몬을 실행중인 특정 프로세스에 9번시그널전달(강제종료)
``` 

----

# kill
 
앞서 말씀드렸듯이 pkill과 kill의 차이점은 없다고 보셔도 무방합니다.
 
 
## 정의
지정된 명령이 실행중인 특정 프로세스에 시그널을 보내는 겁니다.
이 때, 시그널을 입력하지 않으면 디폴트로 15번 시그널(정상작업종료)이 보내집니다.

```
Command#
root@localhost#kill [-Signal] [PID1] [PID2] .......
 
ex)
root@localhost#kill -9 httpd     // httpd 데몬을 실행중인 특정 프로세스에 9번시그널전달(강제종료)
``` 

----

# killall
 
흔히들 kill과 killall명령어를 프로세스를 죽이는 명령어라고 하시는데
반은 맞고 반은 틀립니다. 답은 아래와 같습니다
 
 
## 정의
지정된 명령이 실행중인 모든 프로세스에 시그널을 보내는 겁니다.
이 때, 시그널을 입력하지 않으면 디폴트로 15번 시그널(정상작업종료)이 보내집니다.

``` 
Command#
root@localhost#killall [-Signal] [프로세스명1orPID1] [프로세스명2orPID2] .......
 
ex)
root@localhost#killall -9 httpd  // httpd 데몬을 실행중인 모든 프로세스에 9번시그널전달(강제종료)
```
