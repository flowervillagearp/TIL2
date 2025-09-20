#### There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo via the port 2220. </br>The password for the user bandit28-git is the same as for the user bandit28. </br>Clone the repository and find the password for the next level.

#### bandit27-28 password: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN

### 문제풀이
---
* 27과 같이 /tmp/repo에 비밀번호가 있을줄 알았는데 현재 비밀번호 밖에 없음

* 29 비밀번호를 알려면 clone해야함.

* ssh://bandit28-git@localhost:2220/home/bandit28-git/repo

    - /home/bandit28-git/repo에 클론해도 권한이 없어서 볼수 없음

* ssh://bandit28-git@localhost:2220/tmp/git29

    - /home/bandit28~에 권한이 없어서 /tmp/git29 디렉터리를 만들고 git init후 clone함.

    - Please make sure you have the correct access rights. and the repository exists.

    이런 메세지가 뜨고 클론된 repo폴더를 봐도 비밀번호는 가려져있음.

    ```
    # Bandit Notes
    Some notes for level29 of bandit.

    ## credentials

    - username: bandit29
    - password: xxxxxxxxxx
    ```

* git log명령어로 로그를 보니 제일 최근에 fix info leak라고 커밋된 기록이 있음. 정보 누출을 고친거니 이전에는 정보가 새어나가고 있었던 것처럼 보임

* git show [commit hash] 명령어로 이전 커밋 기록을 보니까 비밀번호가 그대로 쓰여져 있었음.

4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7