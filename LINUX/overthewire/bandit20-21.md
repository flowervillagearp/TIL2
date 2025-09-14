#### There is a setuid binary in the homedirectory that does the following: </br>it makes a connection to localhost on the port you specify as a commandline argument. </br>It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). </br>If the password is correct, it will transmit the password for the next level (bandit21). </br>NOTE: Try connecting to your own network daemon to see if it works as you think

#### bandit19-20 password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

### 문제풀이
---
* 홈 디렉터리에 다음을 수행하는 setuid binary가 있음.
    
    1. 내가 쓴 포트로 localhost와 연결해줌.

    2. 연결한 서버에서 텍스트를 읽어줌. 그리고 이전 레벨의 비밀번호와 비교를 함.

    3. 비밀번호가 맞다면 다음레벨의 비밀번호를 전송함.

* 나의 네트워크에 연결해보고 생각대로 작동하는지 확인

EeoULMCra2q0dSkYj561DX7s1CpBuOBt