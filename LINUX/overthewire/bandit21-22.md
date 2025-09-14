#### A program is running automatically at regular intervals from cron, the time-based job scheduler. </br>Look in /etc/cron.d/ for the configuration and see what command is being executed.

#### bandit20-21 password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt

### 문제풀이
---
* cron이라는 스케줄러에 의해 지정된 시간에 따라 프로그램이 작동함.

* /etc/cron.d/를 살펴보고 어떤 command가 출력되는지 확인

### /etc/cron.d/sysstat
---
#### The first element of the path is a directory where the debian-sa1
#### script is located
PATH=/usr/lib/sysstat:/usr/sbin:/usr/sbin:/usr/bin:/sbin:/bin

#### Activity reports every 10 minutes everyday
5-55/10 * * * * root command -v debian-sa1 > /dev/null && debian-sa1 1 1

#### Additional run at 23:59 to rotate the statistics file
59 23 * * * root command -v debian-sa1 > /dev/null && debian-sa1 60 2

tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q