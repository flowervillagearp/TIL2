#### The password for the next level is stored in a file readme in the homedirectory. </br>Unfortunately, someone has modified [.bashrc](../structure/bashrc.md) to log you out when you log in with SSH.

#### bandit17-18 password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO 

### 문제풀이
---
* bandit18 /home/readme파일에 비밀번호가 있음
* bashrc파일을 변경해서 ssh로 로그인 할 수 없음
---
* bashrc파일을 변경해서 로그인을 막았다면 통신 방법을 변경한다고 될 수 있는게 아닌것같음.

* Commands you may need to solve this level에 ssh, ls, cat을 사용하라고 되어있음.

* ssh bandit18@bandit.labs.overthewire.org -p2220 cat readme 명령어를 입력하면 해당 내용이 리턴됌.

    ssh이후에 cat을 써서 원격 실행하는 방법은 ssh의 일반적인 기능임.
    
    유저 차단 상태에서의 파일을 읽어낸건 관리자의 bashrc설정 미흡으로 보임.

cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8