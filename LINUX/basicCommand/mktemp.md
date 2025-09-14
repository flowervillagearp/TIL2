# mktemp
안전하게 임시 파일이나 디렉토리를 생성하는데 사용.</br>
임시파일을 생성할때 이름 충돌 없이 고유한 이름을 자동으로 생성.</br>
명령 실행시 /temp디렉토리에 고유한 이름의 파일이 생성되고 파일 이름이 리턴됌.</br>
macOS에서는 /var/folders/.../T/ 디렉토리 밑에 만들어짐.</br>
macOS에서는 mktemp -d 는 내부적으로 환경변수 $TMPDIR 을 참고해서 임시 디렉토리를 만듬.</br>

생성된 디렉토리 경로 확인방법: echo $TMPDIR</br>
생성된 디렉토리 하위 파일 확인방법: ls $TMPDIR</br>

이런 임시 파일/폴더들은 macOS에서 알아서 주기적으로 정리해줌.</br>
rm -rf /var/folders/* 같은 명령어로 임시 파일들을 지울수는 있지만 추천X. var폴더 잘못 건드리면 컴 죽음.</br>
굳이 직접 임시파일을 지우고 싶다면 brew cleanup같은 패키지를 쓰는게 더 안전함

### 사용법
---

### option
---
1. d: 파일이 아닌 디렉토리 생성
2. suffix: 특정 확장자를 갖는 파일 생성 // mktemp --suffix ‘.txt’
3. X: X를 파일 이름에 붙이면 X에 임의의 문자가 들어가 파일 이름이 생성됌 // mktemp my-file-XXXX