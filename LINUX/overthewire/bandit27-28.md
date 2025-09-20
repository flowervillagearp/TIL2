#### There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. </br>The password for the user bandit27-git is the same as for the user bandit27. </br>Clone the repository and find the password for the next level.

#### bandit26-27 password: upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB

### 문제풀이
---
* ssh://bandit27-git@localhost/home/bandit27-git/repo

* 위에 git repository가 있음. 2220포트에 연결되어있음.

* bandit-git의 비밀번호는 현재 비밀번호와 같음

Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN

그냥 tmp/repo/README에 나와있는데?

* ~에서 git clone하려니까 권한 오류 나옴

* others에 w권한이 있는 디렉터리 찾아봄.

* tmp디렉터리가 read권한은 없지만 write권한이 있음.

* tmp에 들어가서 git clone함. -> 이미 repo라는 디렉터리가 있다고 나옴.

* cd tmp로 들어가보니 README파일이 있음.

* 읽어보니 비밀번호같은게 있어서 bandit28에 접속해서 입력해보니 들어가짐.

