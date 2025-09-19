#### Good job getting a shell! Now hurry and grab the password for bandit27!

#### bandit25-26 password: s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

### 문제풀이
---
bandit26의 비밀번호를 알았음^ 이제 27의 비밀번호를 알아야 함

bandit26은 접속하자마자 연결이 끊김.

아마 계속해서 vim에서 파일을 탐색해야 할듯

* bandit26에서 했던것처럼 vim에서 /etc/bandit_pass/bandit27 파일을 보려고 했지만 permission denied가 나옴.

* bandit26에서는 bandit25에서 bandit26으로 접속해서 권한이 있었지만 지금은 bandit26으로 접속해서 bandit27을 보려고 하니 권한이 없음.

* commands you may need에 ls명령어만 있는건 파일들을 찾아보라는 뜻일텐데 뭘 찾아야 할지 모르겠음

* 27권한으로 파일을 봐야 할테니 권한을 올릴수 있는 파일을 찾아야 할듯

    - SUID(setuid)로 others의 권한이 rwx인 파일을 찾아보는게 좋을듯 
    
    bandit27이 만들고 다른 유저의 읽기, 쓰기, 실행 권한이 부여되어 있다면 그 프로그램을 통해 27의 권한으로 명령 실행 가능

    ```
    find / -type f -user bandit27 -perm -4000 2>/dev/null
    // type옵션: d(directory), f(file), l(symbolic link)
    ```

    위 명령어로 /경로 밑의 파일중 bandit27유저가 만들었고 4000권한이 있는 파일을 찾아보려 했는데 그런 파일 없다고 뜸

    - 다른 파일 찾아보기
    
* 다른 파일도 없어서 풀이를 찾아보니 쉘을 바꾸라고 되어있음

    bandit26:/usr/bin/showtext
    ```
    #!/bin/sh

    export TERM=linux

    exec more ~/text.txt
    exit 0
    ```
    - showtext가 실행되는 와중에도 vim으로 파일들을 볼수 있는데 쉘을 바꾸는 이유가 뭔지?

    - 일단 쉘을 bash로 바꾸는 방법

        1. vim엥서 :shell 시도.

        2. :shell이 안되면 :set shell=/bin/bash 시도후 :shell 로 쉘 열기

    - vim에서는 ls명령어를 실행해봐도 bandit27파일이 안보였는데 쉘을 바꾸고 보니 bandit27파일이 보임.

    - #### bandit25-26문제에 해당 쉘에서 빠져나오라고 명시해 놨었음...

    - bandit27은 실행파일인데 실행을 하려면 ./bandit27-do [id] 와 같이 명령 실행을 해야함.

    - etc/bandit_pass/bandit27에 비번이 있을텐데 나는 권한이 없으니 읽을수는 없음

    ```
    bandit27-do cat /etc/bandit_pass/bandit27
    ```

    - cat /etc/bandit_pass/bandit27은 permission denied가 나오는데 bandit27-do cat /etc/bandit_pass/bandit27은 실행되는 이유는 bandit26-do파일의 소유자가 bandit27이고 suid비트가 켜진 실행파일이라 그런거임.

    - 그래서 bandit27-do가 실행되는 순간 euid가 bandit27로 바뀜. 당연히 bandit27의 권한으로 접근하니 파일이 읽힘.

    - ls -l, stat, id로 suid비트를 확인 가능함.

upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB