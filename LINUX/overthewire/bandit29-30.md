#### There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo via the port 2220. </br>The password for the user bandit29-git is the same as for the user bandit29.</br>Clone the repository and find the password for the next level.

#### bandit28-29 password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7

### 문제풀이 
---
ssh://bandit29-git@localhost:2220/tmp/fv30/repo

ssh://bandit29-git@localhost:2220/home/bandit29-git/repo

* git clone 후 repo/README.md파일을 보면 아래와 같이 나옴

    ```
    Author: Ben Dover <noone@overthewire.org>
    Date:   Fri Aug 15 13:16:12 2025 +0000

        fix username

    diff --git a/README.md b/README.md
    index 2da2f39..1af21d3 100644
    --- a/README.md
    +++ b/README.md
    @@ -3,6 +3,6 @@ Some notes for bandit30 of bandit.
    
    ## credentials
    
    -- username: bandit29
    +- username: bandit30
    - password: <no passwords in production!>
    ```

    유저 이름만 수정했고 비밀번호는 배포판에는 없음.

    no passwords in production밖에 힌트가 없는것 같음.

    - 배포판에 없으면 개발환경에는 있다는 말일텐데... .......

    - 개발환경을 다른 브랜치에 빼놨나? 개발환경을 분리해놓고 민감정보를 커밋해놨다는것도 이상하긴함.

    - 일단 git show-branch --all명령어로 모든 브랜치들을 확인해봄

    ```
    * [master] fix username
    ! [origin/HEAD] fix username
    ! [origin/dev] add data needed for development
    ! [origin/master] fix username
        ! [origin/sploits-dev] add some silly exploit, just for shit and giggles
    -----
        + [origin/sploits-dev] add some silly exploit, just for shit and giggles
    +   [origin/dev] add data needed for development
    +   [origin/dev^] add gif2ascii
    *++++ [master] fix username
    ```

    - git log origin/dev로 dev branch확인해보니 비밀번호 커밋해놈.ㅉ..

    qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL