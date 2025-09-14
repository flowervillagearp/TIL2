# tr (translate)
지정한 문자를 변환, 삭제하는 명령어

### 사용법
---
tr [option] [set1] [set2] ...

### option
---
1. d: set1에서 지정한 문자를 삭제
2. s: set2에서 반복되는 문자를 삭제
3. t: set1을 set2의 길이로 자름

### example
---
* cat test.txt | tr 'a-z' 'A-Z' // test.txt파일의 소문자를 대문자로 바꿔서 출력
* cat text.txt | tr 'A-Za-z' 'D-ZA-Cd-za-c' // A부터 Z를 D부터 Z, A부터 C로 치환(알파벳을 3칸씩 밀어서 출력)