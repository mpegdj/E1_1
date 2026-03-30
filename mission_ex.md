mpeg46551@c4r3s5 E1_1 % docker run -it -p 80:80 docker/getting-started        
Unable to find image 'docker/getting-started:latest' locally
latest: Pulling from docker/getting-started
c158987b0551: Pull complete 
1e35f6679fab: Pull complete 
cb9626c74200: Pull complete 
b6334b6ace34: Pull complete 
f1d1c9928c82: Pull complete 
9b6f639ec6ea: Pull complete 
ee68d3549ec8: Pull complete 
33e0cbbb4673: Pull complete 
4f7e34c2de10: Pull complete 
Digest: sha256:d79336f4812b6547a53e735480dde67f8f8f7071b414fbd9297609ffb989abc1
Status: Downloaded newer image for docker/getting-started:latest
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/03/30 12:42:11 [notice] 1#1: using the "epoll" event method
2026/03/30 12:42:11 [notice] 1#1: nginx/1.23.3
2026/03/30 12:42:11 [notice] 1#1: built by gcc 12.2.1 20220924 (Alpine 12.2.1_git20220924-r4) 
2026/03/30 12:42:11 [notice] 1#1: OS: Linux 6.17.8-orbstack-00308-g8f9c941121b1
2026/03/30 12:42:11 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 20480:1048576
2026/03/30 12:42:11 [notice] 1#1: start worker processes
2026/03/30 12:42:11 [notice] 1#1: start worker process 30
2026/03/30 12:42:11 [notice] 1#1: start worker process 31
2026/03/30 12:42:11 [notice] 1#1: start worker process 32
2026/03/30 12:42:11 [notice] 1#1: start worker process 33
2026/03/30 12:42:11 [notice] 1#1: start worker process 34
2026/03/30 12:42:11 [notice] 1#1: start worker process 35
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET / HTTP/1.1" 200 8702 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /tutorial/ HTTP/1.1" 200 14807 "http://localhost/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/stylesheets/application.adb8469c.css HTTP/1.1" 200 76332 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/fonts/font-awesome.css HTTP/1.1" 200 30721 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/stylesheets/application-palette.a8b3c06d.css HTTP/1.1" 200 38773 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/javascripts/modernizr.86422ebf.js HTTP/1.1" 200 7296 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/fonts/material-icons.css HTTP/1.1" 200 873 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /css/styles.css HTTP/1.1" 200 892 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /css/dark-mode.css HTTP/1.1" 200 6520 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/javascripts/application.c33a9706.js HTTP/1.1" 200 79589 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /images/docker-labs-logo.svg HTTP/1.1" 200 6469 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /tutorial/tutorial-in-dashboard.png HTTP/1.1" 200 109800 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /fonts/hinted-Geomanist-Book.ttf HTTP/1.1" 200 73568 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/fonts/specimen/MaterialIcons-Regular.woff2 HTTP/1.1" 200 44300 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:44 +0000] "GET /assets/fonts/specimen/FontAwesome.woff2 HTTP/1.1" 200 77160 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"
192.168.215.1 - - [30/Mar/2026:12:42:45 +0000] "GET /assets/images/favicon.png HTTP/1.1" 200 521 "http://localhost/tutorial/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.6 Safari/605.1.15" "-"

지금 보여주신 화면은 도커(Docker)의 입문용 튜토리얼 컨테이너가 아주 성공적으로 실행된 상태입니다!
현재 상황 분석

   1. 이미지 다운로드 및 실행: docker/getting-started 이미지를 인터넷에서 받아와서 사용자의 Mac에서 정상적으로 구동시켰습니다.
   2. 서버 가동: 내부적으로 Nginx 서버가 돌아가며 80번 포트로 접속을 기다리고 있습니다.
   3. 로그 확인: 아래쪽에 나열된 GET / ... 200 로그들은 사용자가 브라우저를 통해 이 서버에 접속했다는 신호입니다. (정상적으로 화면을 불러왔다는 뜻입니다.)

무엇을 확인하면 되나요?
지금 바로 설치하신 크롬(Chrome)이나 Safari 주소창에 아래 주소를 입력해 보세요.

http://localhost

도커 사용법을 알려주는 한글/영어 웹 페이지가 뜬다면 완벽하게 성공한 것입니다.
작업 중단 방법
이 터미널은 현재 도커 실시간 로그를 보여주는 상태라 다른 명령어를 입력할 수 없습니다.

* 중단하려면: 터미널 창에서 Control + C를 누르면 컨테이너가 멈추고 다시 명령어를 입력할 수 있는 상태로 돌아옵니다.
* 백그라운드 실행: 만약 터미널을 계속 쓰고 싶으면서 도커도 띄워놓고 싶다면, 나중에 명령어를 실행할 때 -d 옵션을 붙여 docker run -d -p 80:80 docker/getting-started라고 입력하면 됩니다.

이제 웹 브라우저에서 튜토리얼 페이지가 잘 뜨는지 확인해 보시겠어요?

아니요, 지금 상황에서는 도커 컨테이너도 함께 멈춘 상태입니다.
터미널에서 docker run 명령어를 입력할 때 -it(대화형) 옵션을 사용했기 때문입니다. 이 방식은 터미널과 도커가 한 몸처럼 연결되어 있어서, Control + C로 프로세스를 종료하면 도커 컨테이너도 즉시 종료됩니다.
확인 방법
정말 꺼졌는지 확인하려면 터미널에 아래 명령어를 입력해 보세요.

docker ps


* 목록에 아무것도 뜨지 않는다면 종료된 것입니다.
* 꺼진 컨테이너까지 다 보려면 docker ps -a를 입력하면 됩니다.

------------------------------
터미널을 끄지 않고 배경에서 계속 돌리고 싶다면? (추천)
터미널을 자유롭게 쓰면서 도커도 계속 띄워두고 싶다면, -d (detached) 옵션을 추가해야 합니다.

   1. 다시 실행할 때:
   
   docker run -d -p 80:80 docker/getting-started
   
   * 이렇게 실행하면 긴 문자열(ID)만 출력되고 바로 다음 명령어를 입력할 수 있는 상태가 됩니다.
   2. 배경에서 돌아가는 도커 끄기:
   * docker ps로 구동 중인 컨테이너 ID를 확인합니다.
      * docker stop [컨테이너ID]를 입력하면 안전하게 꺼집니다.
   
이제 -d 옵션을 넣어서 다시 실행해 보시겠어요? 아니면 종료된 컨테이너를 다시 살리는 방법이 궁금하신가요?

