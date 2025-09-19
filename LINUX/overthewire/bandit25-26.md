#### Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. </br>Find out what it is, how it works and how to break out of it. </br>NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. </br>You should use command prompt instead.

#### bandit24-25 password: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

### 문제풀이
---
* ./bandit26.sshkey로 bandit26 접속.
* bandit26 shell은 bin/bash가 아님 이건 직접 알아봐야함.

ssh bandit26@bandit.labs.overthewire.org -p 2220

ssh bandit26@bandit.labs.overthewire.org -p 2220 -i ./bandit26.sshkey

ssh user@host 'ps -p $$ -o comm='

* bandit26에 접속하면 바로 접속 끊김.

    왜 끊기나. // 

* echo $0로 쉘을 확인할수는 있지만 사용중인 쉘에서 명령어를 입력해야 함. </br> bandit26은 바로 연결이 끊어져서 echo $0로 쉘 확인이 안됌.

bandit26:/usr/bin/showtext
```
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```

* vi 에서 :e 명령어 -> 현재파일 저장후 새로운 파일 열기

* :e /file -> 현재 파일 저장후 해당 파일 열기

* :e /etc/bandit_pass/bandit26

s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

---

#### ssh로 접속 성공인데 즉시 종료됌

* 서버에서 비밀번호/키 인증은 성공. 하지만 shell프롬프트 없이 연결이 끊김.

* 이 현상은 로그인 shell이 진짜 shell이 아니라 연결 즉시 종료하는 프로그램일 가능성이 큼.

* 로그인 shell이 /usr/bin/showtext같은 shell이 아니라 실행파일로 되어있음을 보면 더 확실해짐.

* more ~/text.txt exit 0코드를 보면 페이저가 한 화면에 다 나오면 바로 끝나버린다는 뜻 같음

* 그럼 페이저를 인터랙티브로(명령어를 쓸수 있는 상태) 만들면? 화면에 페이지가 다 안나온다면 안끝나는거 아님?

* 인터랙티브로 들어오면 키 바인딩을 쓸 수 있음. h(도움말) v(편집기) e(다른 파일 열기)등.

* showtext가 bandit26 권한으로 more/less를 띄우기 때문에, 그 안에서 여는 파일 접근도 해당 권한으로 시도됌.

* 그러니 less/more페이지에서 v -> vi or vim이 실행되면 
    ```
    :e /etc/bandit_pass/bandit26
    ```
    명령어로 파일을 열어 내용을 확인할수 있음.

#### 어떻게 비밀번호 파일을 찾나

* bandit문제에 etc/bandit_pass/bandit** 라는 식의 절대 경로를 알려주지만 문제를 푸는 상황이 아닐때는 어떻게 찾을까.

* vim에는 netrw플러그인이 포함되어 있을거임. 이걸로 디렉터리를 볼수 있음.
    ```
    :Explore // 현재 디렉터리 탐색
    :Explore /etc // /etc로 바로 이동
    //방향키, 엔터로 탐색, -로 상위 이동.
    ```

* vim에서는 shell명령어도 실행 됌
    ```
    :!ls -la /etc
    :!ls -la /etc/bandit_pass
    // 이런식으로 하위 구조를 볼수도 있음
    ```

