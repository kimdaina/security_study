오늘 목표(2026-07-14)

# Bandit

## Level 14

<pre>
    사용한 명령어
    - ssh
    - nc
    - telnet


    배운 것

    telnet [port] [hostname]
    - 다른 컴퓨터에서 특정 컴퓨터로 원격접속을 할 수 있도록 도와주는 표준 프로토콜

    nc 
    - netcat의 줄임말로 telnet과 비슷 , * TCP 연결
    
</pre>

<pre>
    *
        차이점으로는 telnet은 한 줄 한 줄씩 보내는 반면 nc는 스트림으로 보내야 한다.
        telnet localhost 30000 하고 bandit14의 비번을 붙여넣기하면 bandit15의 비번이 나옴
        
        nc는 nc localhost 30000이렇게 하면 접속이 안되고 일단 30000번 포트를 열어야하기 때문에 
        nc -l 30000
        nc localhost 30000 이렇게 순서대로 해야한다

</pre>

## Level 15

<pre>
    사용한 명령어
    - openssl
    
    배운 것

    openssl
    - SSL/TLS 인증서 발급, 개인키 생성, 암·복호화 등을 수행하는 필수적인 명령줄 도구

    openssl s_client [옵션] [호스트:포트]
    - s_client는 openssl 안에 들어가있는 여러 기능 중 하나로, SSL Client 즉 SSL서버에 접속하는 클라이언트 프로그램이라는 뜻임
    
</pre>

<pre>
    *
        nc명령어는 기본적으로 SSL/TLS를 지원하지 않음

        openssl s_client -connect localhost:30001
        여기서 -connect라는 옵션은 어디에 연결할지 지정하는 옵션

        TCP - 데이터를 주고받을 수 있게 해줌 (BUT 내용을 숨기지 않음)
        SSL - TCP위에 덧씌우는 암호화

        이 문제에서는 내가 30001포트에 접속해서 데이터를 보내야하기 때문에 '클라이언트'를 사용
</pre>

## Level 16

<pre>
    사용한 명령어
    - nmap

    배운 것

    nmap -p [포트 번호] [대상 IP]
    - 네트워크 탐지 및 보안 감사에 사용되는 네트워크 스캐너

    nmap -sV [대상 IP] -p [포트번호]
    -
    옵션:
        -sV :  서비스 버전 탐지 (Service Version Detection)
                열려 있는 포트에서 무슨 서비스가 동작 중인지, 그 서비스의 정확한 이름과 버전을 식별

</pre>

<pre>
    *
        -p뒤에는 무조건 포트 번호가 와야됨
        특정 포트 지정 : -p [확인할 포트] 
        범위 지정 : -p [시작번호-끝번호]

        nmap 명령어를 입력해서 열려있는 포트(그 중에서도 ssl을 이용하는 포트) 를 찾은 뒤
        Level 14처럼 openssl s_client를 이용하여 연결

        이 문제는 비번이 아니라 sshkey를 줌 Level 13처럼 ssh로연결

        비밀번호에 k가 포함되어 있으면, TLS 명령어인 KEYUPDATE로 인식되어 연결이 끊김 때문에 아래 명령어 사용
        openssl s_client -connect localhost:<포트번호> -ign_eof
</pre>

-----------------------------------------------------

후기 : 이제 업그레이드됨 진짜 하루에 꼬박꼬박 해야하는데,,