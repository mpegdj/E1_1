# E1_1 미션 연습 자료

이 README는 `/readme_ref.md`와 `/docs/mission_intro.md`를 참고하여 작성한 미션 수행 연습 문서입니다.

## 1. 미션 개요

- 목표: 개발 워크스테이션 환경에서 터미널, Docker, Git/GitHub를 활용해 재현 가능한 실행 환경을 구성하고 검증합니다.
- 핵심 활동:
  - 터미널과 파일 시스템 기본 조작
  - 파일/디렉터리 권한 실습
  - Docker 설치 및 기본 명령 점검
  - Docker 컨테이너 실행 및 로그 확인
  - Dockerfile 기반 커스텀 웹 서버 이미지 빌드
  - 포트 매핑 접속 확인
  - 바인드 마운트와 Docker 볼륨 검증
  - Git 사용자 설정 및 GitHub 연동

## 2. 실행 환경

- OS: macOS
- Shell: zsh
- Docker: `docker --version`로 버전 확인
```bash
mpeg46551@c5r1s2 ~ % docker --version
Docker version 28.5.2, build ecc6942
```
- Git: `git --version`로 버전 확인
```bash
mpeg46551@c5r1s2 ~ % git --version
git version 2.53.0
```

## 3. 수행 항목

- [x] 터미널 기본 조작: 현재 위치, 파일/디렉터리 생성·이동·삭제, 내용 확인
- [x] 권한 실습: 파일 1개와 디렉터리 1개에 대해 권한 변경 전/후 비교
- [x] Docker 설치 및 실행 점검: `docker --version`, `docker info`
- [x] Docker 이미지/컨테이너 조회: `docker images`, `docker ps -a`
- [x] `hello-world` 실행 성공 확인
- [x] `ubuntu` 컨테이너 내부 진입 후 `ls`, `echo` 실행
- [x] `docker attach`와 `docker exec` 차이 관찰
- [x] Dockerfile 기반 커스텀 웹 서버 이미지 빌드
- [x] 포트 매핑으로 웹 접속 확인
- [x] 바인드 마운트 파일 변경 반영 확인
- [x] Docker 볼륨 영속성 검증
- [x] Git 설정 및 GitHub 연동

## 4. 수행 방법 및 예시

### 4.1 터미널 기본 조작

```bash
mpeg46551@c5r1s2 ~ % cd ~

mpeg46551@c5r1s2 ~ % pwd

mpeg46551@c5r1s2 ~ % ls    
Desktop		Downloads	Library		Music		Pictures
Documents	E1_1		Movies		OrbStack	Public


mpeg46551@c5r1s2 ~ % ls -a
.			.lesshst		Downloads
..			.orbstack		E1_1
.CFUserTextEncoding	.ssh			Library
.DS_Store		.vscode			Movies
.Trash			.zsh_history		Music
.copilot		.zsh_sessions		OrbStack
.docker			Desktop			Pictures
.gitconfig		Documents		Public

mpeg46551@c5r1s2 ~ % cd E1_1
mpeg46551@c5r1s2 E1_1 % ls -al
total 72
drwxr-xr-x  10 mpeg46551  mpeg46551    320 Apr  4 15:56 .
drwxr-x---+ 24 mpeg46551  mpeg46551    768 Apr  4 15:57 ..
drwxr-xr-x  16 mpeg46551  mpeg46551    512 Apr  4 15:48 .git
-rw-r--r--   1 mpeg46551  mpeg46551   4614 Apr  4 15:59 README.md
drwxr-xr-x   4 mpeg46551  mpeg46551    128 Apr  3 21:39 docker1
drwxr-xr-x  10 mpeg46551  mpeg46551    320 Apr  4 15:45 docs
-rw-r--r--   1 mpeg46551  mpeg46551   9929 Apr  2 19:13 e1_1.md
drwxr-xr-x   3 mpeg46551  mpeg46551     96 Apr  2 19:13 logs
-rw-r--r--   1 mpeg46551  mpeg46551  12332 Apr  4 15:56 readme_ref.md
drwxr-xr-x   3 mpeg46551  mpeg46551     96 Apr  2 19:13 test-dir

$ mkdir test-dir

$ ls
app/  docs/  e1_1.md  logs/  README.md  test-dir/

$ cd test-dir

$ pwd
/d/git/E1_1/test-dir

$ touch hello.md

$ ls
hello.md

$ cat hello.md

$ echo "hello codyssey" >> hello.md

$ cat hello.md
hello codyssey

$ cp hello.md hello1.md

$ ls
hello.md  hello1.md

$ mv hello1.md hello2.md

$ ls
hello.md  hello2.md

$ rm hello2.md

$ ls
hello.md

```

### 4.2 권한 실습
| 구분 | 권한 기호 | (rwx),의미 |
| --- | --- | ---|
| -| 일반적인 파일 | 텍스트, 이미지, 실행 파일 등)을 의미합니다.
|d | 디렉토리 | (Directory), 즉 폴더를 의미합니다.|
| l |  바로가기 | 아이콘 같은 심볼릭 링크를 의미합니다. |
|r| Read | 읽기 권한 (내용 보기) |
|w | rite | 쓰기 권한 (수정, 삭제) |
| x |Execute | 실행 권한 (프로그램 실행) |
| - | None | 해당 권한 없음 |

```bash
mpeg46551@c5r1s2 E1_1 % cd test-dir
mpeg46551@c5r1s2 test-dir % echo "sample" >> sample.txt
mpeg46551@c5r1s2 test-dir % ls -l
total 16
-rw-r--r--  1 mpeg46551  mpeg46551  15 Apr  2 19:13 hello.md
-rw-r--r--  1 mpeg46551  mpeg46551   7 Apr  4 16:10 sample.txt
mpeg46551@c5r1s2 test-dir % chmod 744 sample.txt
mpeg46551@c5r1s2 test-dir % ls -l
total 16
-rw-r--r--  1 mpeg46551  mpeg46551  15 Apr  2 19:13 hello.md
-rwxr--r--  1 mpeg46551  mpeg46551   7 Apr  4 16:10 sample.txt

mpeg46551@c5r1s2 test-dir % mkdir folder
mpeg46551@c5r1s2 test-dir % ls -l
total 16
drwxr-xr-x  2 mpeg46551  mpeg46551  64 Apr  4 16:15 folder
-rw-r--r--  1 mpeg46551  mpeg46551  15 Apr  2 19:13 hello.md
-rwxr--r--  1 mpeg46551  mpeg46551   7 Apr  4 16:10 sample.txt
```


### 4.3 Docker 설치 및 점검

```bash
brew install --cask docker  #표준
brew install --cask orbstack #작고 빠름
mpeg46551@c5r1s2 test-dir % docker --version
Docker version 28.5.2, build ecc6942

mpeg46551@c5r1s2 test-dir % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/mpeg46551/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
```

### 4.4 기본 Docker 명령

```bash
mpeg46551@c5r1s2 test-dir % docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    e2ac70e7319a   11 days ago   10.1kB

mpeg46551@c5r1s2 test-dir % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED        STATUS                    PORTS     NAMES
c9c920c75fc0   hello-world   "/hello"   19 hours ago   Exited (0) 19 hours ago             friendly_yalow

mpeg46551@c5r1s2 test-dir % docker logs c9c920c75fc0

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:

```


### 4.5 `hello-world` 및 `ubuntu`

```bash
mpeg46551@c5r1s2 test-dir % docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
817807f3c64e: Pull complete 
Digest: sha256:186072bba1b2f436cbb91ef2567abca677337cfc786c86e107d25b7072feef0c
Status: Downloaded newer image for ubuntu:latest 

root@aef087afd862:/# ls  
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@aef087afd862:/# exit
exit

mpeg46551@c5r1s2 test-dir % 

mpeg46551@c5r1s2 test-dir % docker images 
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    e2ac70e7319a   11 days ago   10.1kB
ubuntu        latest    f794f40ddfff   5 weeks ago   78.1MB

mpeg46551@c5r1s2 test-dir % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
aef087afd862   ubuntu        "bash"     4 minutes ago   Exited (0) 2 minutes ago             musing_germain
c9c920c75fc0   hello-world   "/hello"   19 hours ago    Exited (0) 19 hours ago              friendly_yalow

mpeg46551@c5r1s2 test-dir % docker logs aef087afd862
  
root@aef087afd862:/# ls  
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

mpeg46551@c5r1s2 test-dir % docker stats --no-stream
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS
```

### 4.6 Dockerfile 기반 커스텀 이미지

- 베이스 이미지: `nginx` 또는 `nginx:stable-alpine`
1. nginx vs nginx:stable-alpine (무엇을 고를까?)
이 둘은 똑같은 웹 서버 프로그램(nginx)이지만, 그 밑바탕이 되는 **'OS의 무게'**가 다릅니다.

nginx (표준형):

**데비안(Debian)**이라는 리눅스를 기반으로 합니다.

우리가 흔히 쓰는 명령어(ls, cat, apt-get 등)가 다 들어있어 사용하기 편하지만, 용량이 큽니다 (약 100MB 이상).

nginx:stable-alpine (경량형 / 추천!):

**알파인(Alpine)**이라는 초경량 리눅스를 기반으로 합니다.

보안에 꼭 필요한 기능만 남기고 다 깎아냈습니다.

용량이 매우 작습니다 (약 10~20MB). 아이맥의 용량을 아끼고 속도를 높이려면 보통 이걸 씁니다.
- 커스텀 포인트: 정적 `index.html` 추가, `EXPOSE`, `CMD` 설정

- 빌드 예시:

```bash
mpeg46551@c5r1s2 docker1 % docker build -t my-web-img .
[+] Building 7.7s (7/7) FINISHED                                                                                                                                        docker:orbstack
 => [internal] load build definition from Dockerfile  0.2s
 => => transferring dockerfile: 792B    0.0s
 => [internal] load metadata for docker.io/library/nginx:stable-alpine    2.8s
 => [internal] load .dockerignore     0.1s
 => => transferring context: 2B      0.0s
 => [internal] load build context     0.2s
 => => transferring context: 192B  

 mpeg46551@c5r1s2 docker1 % docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
my-web-img    latest    f228a01c58c9   5 minutes ago   62.1MB
hello-world   latest    e2ac70e7319a   11 days ago     10.1kB
ubuntu        latest    f794f40ddfff   5 weeks ago     78.1MB
mpeg46551@c5r1s2 docker1 % 
```

- 실행 예시:

```bash
docker run -d -p 8080:80 --name web-test my-web-img
curl -s http://localhost:8080

mpeg46551@c5r1s2 docker1 % docker rm -f web-test
web-test

mpeg46551@c5r1s2 docker1 % docker build -t my-web-img .
[+] Building 2.5s (7/7) FINISHED                                                              docker:orbstack

mpeg46551@c5r1s2 docker1 % docker run -d -p 8080:80 --name web-test my-web-img
f2a3be15ba2d15ef12f405a0427dd0b7f2eefc83f38ca269172b7fdfcbd86e52

mpeg46551@c5r1s2 docker1 % curl -s http://localhost:8080                      
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>My Docker Web</title>
</head>
<body>
    <h1>Hello Codyssey!</h1>
    <p>Docker 컨테이너에서 실행 중인 웹 서버입니다.</p>
</body>
</html>%  
```

1. -it (대화형 모드)
* 언제 쓰나요? 아까처럼 ubuntu 리눅스 안으로 직접 들어가서 명령어를 치고, 파일 권한(ls -l)을 확인하는 등 **"나랑 리눅스가 실시간으로 대화"**해야 할 때 씁니다.

특징: 터미널 창이 리눅스 화면으로 바뀝니다. exit를 치고 나오면 컨테이너도 보통 같이 종료됩니다.

2. -d (백그라운드 모드 / 데몬)
* 언제 쓰나요? 지금 만드신 nginx 웹 서버처럼, 내가 터미널에서 다른 작업을 하는 동안에도 "뒤에서 조용히 계속 돌아가고 있어야 할 때" 씁니다.

* 의미: detached(분리된)의 약자입니다. 터미널과 컨테이너를 분리해서 뒤편(백그라운드)에서 실행시킨다는 뜻이에요.

* 특징: 명령어를 쳐도 리눅스 안으로 들어가지 않고, 바로 다시 원래의 아이맥 터미널(%)로 돌아옵니다. 하지만 웹 서버는 뒤에서 열심히 돌아가고 있죠.

3. -p (포트 포워딩)
* 언제 쓰나요? 컨테이너 외부(내 아이맥)에서 내부(웹 서버)로 "접속할 통로를 뚫어줄 때" 씁니다.
* 구성: -p [내 아이맥 포트]:[컨테이너 내부 포트]
* 예: -p 8080:80 → "내 아이맥 8080번으로 들어오면 컨테이너 80번으로 보내줘!"

### 4.7 포트 매핑 확인
```bash
mpeg46551@c5r1s2 docker1 % docker ps
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES
f2a3be15ba2d   my-web-img   "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-test
```

* 💡 주의: -p 80:8080 vs -p 8080:80
* 질문하신 내용에서 포트 순서도 매우 중요합니다! 보통은 이렇게 씁니다.
* docker run -p [내 아이맥 포트]:[컨테이너 내부 포트]
* -p 80:8080: (내 아이맥의 80번 포트)를 (컨테이너의 8080번)으로 연결해라!
* -p 8080:80: (내 아이맥의 8080번 포트)를 (컨테이너의 80번)으로 연결해라!
* 만약 Nginx 베이스 이미지를 쓰신다면 컨테이너 내부는 보통 80번을 쓰므로, 보통은 -p 8080:80 형식을 가장 많이 사용하게 됩니다.
```bash

```

### 4.8 바인드 마운트
$(pwd)/app : /usr/share/nginx/html : ro

$(pwd)/app (왼쪽 - 내 아이맥): * "지금 내가 터미널에서 작업 중인 폴더 안에 있는 app 폴더를 써라!"라는 뜻입니다.

$(pwd)는 "내 현재 위치 전체 주소"를 자동으로 채워주는 단축키 같은 거예요.

/usr/share/nginx/html (오른쪽 - 도커 컨테이너): * "도커(Nginx)야, 네가 원래 웹 파일을 읽어가는 그 정해진 폴더 있지? 거길 내 폴더로 덮어써!"라는 뜻입니다.

ro (옵션): * "도커는 내 파일을 **읽기(Read-Only)**만 해! 수정은 못 하게 막아줘."라는 뜻입니다. (안 써도 되지만 안전을 위해 씁니다.)
```bash
mpeg46551@c5r1s2 docker1 % docker run -d -p 8080:80 -v "$PWD/app:/usr/share/nginx/html:ro" --name web-bind my-web-img
33095333ff1264432f1d4fc2a4355f8b9edb3daba83b1f80008ce58bd7f766a7
docker: Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint web-bind (28e925a8c4ca8007ddad5408fe70c8e54ef651a0c9a16214309a522f92e492de): Bind for 0.0.0.0:8080 failed: port is already allocated

mpeg46551@c5r1s2 docker1 % docker rm -f web-bind
web-bind

mpeg46551@c5r1s2 docker1 % docker run -d -p 8080:80 -v "$PWD/app:/usr/share/nginx/html:ro" --name web-bind my-web-img  
2367aa0e0c90144e1db324fd10830d87b9ce725be07d2be36709e8899ddd7641

mpeg46551@c5r1s2 docker1 % docker ps -a                                                                                
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES
2367aa0e0c90   my-web-img   "/docker-entrypoint.…"   10 seconds ago   Up 10 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-bind

```
# 호스트에서 app/index.html 수정 후 컨테이너 내부 확인
```

### 4.9 Docker 볼륨

```bash
docker volume create my-data
docker run -d --name vol-test -v my-data:/data ubuntu sleep 3600
docker exec vol-test sh -c "echo hello > /data/hello.txt"
docker rm -f vol-test
docker run --rm --name vol-test2 -v my-data:/data ubuntu ls /data
```

### 4.10 Git 및 GitHub

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --list
```

- GitHub 연동: VS Code Git 확장 또는 명령어로 원격 저장소 추가
- 민감 정보 노출 주의: 토큰, 비밀번호, 개인키는 문서에 포함하지 않습니다.

## 5. 검증 기준

- `README.md`에 수행 결과와 명령 기록이 포함되어 있어야 함
- Docker 명령의 출력과 검증 경로가 명확히 기록되어야 함
- 포트 매핑, 바인드 마운트, 볼륨 검증 결과가 존재해야 함
- Git 설정 결과 및 GitHub 연동 여부를 문서에서 확인할 수 있어야 함

## 6. 참고

- 이 문서는 `/readme_ref.md`의 기술 문서 구성 예시와 `/docs/mission_intro.md`의 미션 목표 및 검증 요구사항을 참고하여 작성되었습니다.
- 실제 수행 내용은 추가 로그 파일 또는 명령 출력 기록을 `logs/` 폴더에 정리하여 연동하면 좋습니다.

## 7. 추가 권장 사항

- `logs/` 폴더에 터미널/도커/깃 수행 로그를 분리하여 기록
- `docker-compose.yml`을 작성해 보너스 과제인 Compose 연습 수행
- GitHub 원격 저장소 주소와 제출 형식을 README에 명확히 추가
