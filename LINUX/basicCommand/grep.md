# grep
특정 파일에서 지정한 문자열이나 정규표현실을 포함한 생을 출력해주는 명령어. tail, ls등의 명령어와 주로 조합/응용함

### 사용법
---
grep [option] [pattern] [filename] [filename2] ...

### option
---
1. c: 일치하는 행의 수 출력
2. i: 대소문자 구별X
3. v: 일치하지 않는 행만 출력
4. n: 포함된 행의 번호를 함께 출력
5. I: 패턴이 포함된 파일의 이름을 출력
6. w: 단어와 일치하는 행만 출력
7. x: 라인과 일치하는 행만 출력
8. r: 하위 디렉터리를 포함한 모든 파일에서 검색
9. m [number]: 최대로 표시될 수 있는 결과를 제한
10. E: 찾을 패턴을 정규 표현식으로 찾음
11. F: 찾을 패턴을 문자열로 찾음

### example
---
* tail -f mylog.log | grep 192.143.12.43 // mylog파일을 실시간 엑세스 하고 ip주소가 192.143.12.43인 행만 추출
* cat mylog.txt | grep 'Apple' | grep 'Banana' // mylog.txt파일에서 Apple과 Banana가 있는 문자열ㅇ르 찾음
* grep -m 100 'Apple' mylog.txt // mylog.txt파일에서 Apple문자열을 100개 까지만 찾기
