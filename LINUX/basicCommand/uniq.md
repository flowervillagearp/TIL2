# uniq
연속적으로 반복되는 행을 한 행으로 줄여주는 명령어. sort명령어로 정렬 후 uniq로 생략하는 방식으로 많이 씀

### 사용법
---
uniq [optioin] [filename]

### option
---
1. c: 연속적으로 반복된 수를 행 앞에 표시
2. u: 연속적으로 반복되지 않은 행만 출력
3. d: u와 반대로 반복된 행들만 한번 출력
4. i: 대/소문자를 구별하지 않고 정렬

### example
* cat data.txt | sort | uniq -u data.txt // data.txt파일에서 한번만 나오는 문자열을 정렬