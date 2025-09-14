#### The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000.</br>First find out which of these ports have a server listening on them.</br> Then find out which of those speak SSL/TLS and which don’t.</br> There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

#### bandit15-16 password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

### 문제풀이
---
*  현재 레벨의 비밀번호를 제출하면 다음 단계의 키를 받음.
---
* localhost port 31000 ~ 32000로 제출해야함.
---
1. localhost가 어떤 port에 접속중인지 확인.

* nmap으로 확인하는 방법

    command
    ```
    nmap -sV -p 31000-32000 localhost
    ```
    return value
    ```
    PORT      STATE SERVICE     VERSION
    31046/tcp open  echo
    31518/tcp open  ssl/echo
    31691/tcp open  echo
    31790/tcp open  ssl/unknown
    31960/tcp open  echo
    ```

---
2. 그중 어떤 포트가 SSl/TLS를 사용중인지 확인.

    31518, 31790이 ssl을 사용중이니 localhost의 31518, 31790 port로 연결해서 현재 비밀번호를 제출

    ```
    openssl s_client -connect localhost:31790
    ```

    ```
    openssl s_client -connect localhost:31518
    ```
    연결 후 비밀번호를 입력하면 KEYUPDATE메세지가 나오는데 tls1.3부터 나오는 알림임.

    -ign_eof옵션을 붙혀서 값이 안나오는 문제를 해결할수는 있었는데 무슨 문제인지, 왜 해결됬는지는 모름

    ```
    openssl s_client -connect localhost:31790 -ign_eof
    ```
    위 명령어로 private key를 받을수 있음.

    받은 키를 복사해서 /tmp 디렉터리에 새로운 디렉터리와 파일을 만들고 붙혀넣기
    ```
    cd /tmp
    mkdir/keydir
    vim pkey
    ```

    /home/bandit16/ 에서 디렉터리를 만드려고 하면 permission denied가 나오는데 /tmp에 만들수 있는 이유는 모르겠음.

    ssh로 만든 키 파일을 이용해 bandit17에 연결
    ```
    ssh -i ./pkey bandit17@localhost
    ```

    그럼 아래와 같은 에러메세지가 나옴
    ```
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    Permissions 0664 for 'pkey' are too open.
    ```

    chmod로 파일 권한을 600으로 설정해줌

    이후 ~경로에서 ssh로 bandit17에 접속
    ```
    ssh -i /tmp/keydir/pkey bandit17@localhost -p 2220
    ```


---
* 하나의 서버만 다음단계의 키를 리턴해줌.
---

EReVavePLFHtFlFsjn3hyzMlvSuSAcRD