toy_project_linux

--------------------------
GUI => 크롬 접속
filebrowser 설치
>>  curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash filebrowser -r /path/to/your/files

main 함수에 server, input , Gui 생성
---------------------------------------

exec + fork로 webserver , systemserver,  input , gui ==> switch case로 구현

input 부분에 segfault 처리 핸들러 구현
	=> input process 죽으면 콜스택 유발(pid로 kill시)
main 프로세스 부분에서 자식 프로세스 시그널 출력

--------------------------------------
멀티 스레드 추가하기(구상)
- 메인 함수
==> GUI
==> Web Server : Frontend + Backend
==> Systemserver(와치독 스레드+ 모니터 스레드 + 카메라 스레드 + 디스크 스레드)
==> Input Process : 커맨드 스레드 + 센서 스레드
이외에 다바이스 드라이버 등등 Kernel Level 구현 예정

input.c => toy_loop 추가 (명령어 옵션)
create thread + 예외처리 : assert 함수로 구현
---------------------------------------
공유되는 전역변수에 대한 뮤텍스락 구현 
--------------------------------------
C ++ 연동 추가 (HAL)

-- GUI (구글 브라우저)

-- 웹 서버 : 프론트엔드 + 백엔드

-- 메인함수
-- 시스템 서버 : 와치독, 모니터, 카메라(HAL의 API호출), 디스크스레드
-- 인풋 프로세스 : 센서스레드 , 커맨드 스레드
-- HAL (카메라 HAL) : C++ 연동을 위함
이외에디바이스 드라이버 등등 Kernel Level 구현 예정
--------------------------------------
System Server쪽 disk thread 구현 
-------------------------------------
스레드별 message queue 구현 , input(command thread <=> system server thread)

------------------------------------
타이머 부분 세마포어) 시그널 발생시 세마포어 post하여 스레드 깨우기

------------------------------------------
센서스레드, 센서정보  => 공유메모리 => 공유메모리 key를 메시지 큐에 넣어서 모니터 스레드에 보내기 (시스템 서버 프로세스)

step1 : 공유메모리 사전작업 , create,attach 등등 및 헤더파일 작성

step2 : 공유메모리 생성, 메시지큐로 모니터 스레드 접근하여 공유메모리에서 센서정보 출력

---------------------------------------
mmap 구현하기 => elf 파일 내용  출력

---------------------------------------
fs폴더의 사이즈 체크하는 디스크 서비스 스레드 구현하기

----------------------------------------


