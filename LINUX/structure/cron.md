# cron
리눅스 계열에서 특정 시간에 특정 작업을 하는 [daemon](./daemon.md)을 크론(cron)이라 하고 크론이 언제 무엇을 하는지 특정 파일에 저장하는 것을 크론탭(crontab)이라고 함.</br>

### 크론탭 사용법
---
1. crontab -e: 크론탭 편집
2. crontab -l: 크론탭 작업 내용 확인
3. crontab -r: 크론탭 삭제
4. service cron start: 크론탭 시작
5. service cron stop: 크론탭 중지
6. service cron status: 크론탭 작동 확인

### 크론탭 주기 설정
---
*****[command]

분시일월요일[command]

분: 0-59

시: 0-23

일: 0-31

월: 0-12

요일: 0-6 (0=일요일-6=토요일)

#### example
---
***** [command] // 매 분마다 실행

1**** [command] // 매 분마다 실행

0 13 * * * [command] // 매일 13시에 실행