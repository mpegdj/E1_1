
# 🧪 DevOps 개발 워크스테이션 구축

---

## 1. 📌 프로젝트 개요

본 프로젝트는 터미널, Docker, Git을 활용하여
재현 가능한 개발 환경(Development Workstation)을 구축하는 것을 목표로 한다.

주요 목표:

* CLI 기반 파일/권한 관리 이해
* Docker 컨테이너 실행 및 관리
* Dockerfile을 통한 커스텀 이미지 생성
* 포트 매핑, 마운트, 볼륨 개념 이해
* Git/GitHub 기반 협업 환경 구성

---

## 2. ⚙️ 실행 환경

| 항목       | 내용                             |
| -------- | ------------------------------ |
| OS       | (macOS / Ubuntu)  |
| Shell    | ( zsh)                |
| Terminal | (예: iTerm2 / Windows Terminal) |
| Docker   |                                |
| Git      |                                |

```bash
docker --version  # Docker 버전 확인
# 출력 결과 붙여넣기

docker info  # Docker 시스템 전체 상세 정보 확인
# 출력 결과 붙여넣기

git --version  # Git 버전 확인
# 출력 결과 붙여넣기
```

---

## 3. ✅ 수행 체크리스트

* [ ] 터미널 기본 조작
* [ ] 파일/디렉토리 생성 및 관리
* [ ] 권한 변경 실습
* [ ] Docker 설치 및 점검
* [ ] hello-world 실행
* [ ] ubuntu 컨테이너 진입
* [ ] Docker 기본 명령 실행
* [ ] Dockerfile 기반 이미지 빌드
* [ ] 포트 매핑 접속 확인
* [ ] 바인드 마운트 실습
* [ ] Docker 볼륨 영속성 검증
* [ ] Git 설정
* [ ] GitHub 연동

---

## 4. 🖥️ 터미널 조작 로그

### 📂 기본 명령어

```bash
pwd  # 현재 작업 중인 디렉토리의 절대 경로 출력
ls -la  # 숨김 파일을 포함한 디렉토리 내 모든 파일과 권한 정보 상세 출력
mkdir test-dir  # 'test-dir'이라는 이름의 새로운 디렉토리 생성
cd test-dir  # 'test-dir' 디렉토리로 이동
touch file.txt  # 빈 파일 'file.txt' 생성 (또는 기존 파일의 시간 정보 업데이트)
cp file.txt file_copy.txt  # 'file.txt'를 복사하여 'file_copy.txt' 생성
mv file_copy.txt file2.txt  # 'file_copy.txt'의 이름을 'file2.txt'로 변경 (또는 이동)
rm file2.txt  # 'file2.txt' 파일 삭제
```

👉 결과:

```bash
mpeg46551@c5r1s2 ~ % cd ~

mpeg46551@c5r1s2 ~ % pwd
/Users/mpeg46551

mpeg46551@c5r1s2 ~ % mkdir e1_1

mpeg46551@c5r1s2 ~ % ls 
Desktop		Downloads	Library		Music		Pictures
Documents	E1_1		Movies		OrbStack	Public

mpeg46551@c5r1s2 ~ % cd e1_1
mpeg46551@c5r1s2 e1_1 % 

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

### 📄 파일 내용 확인

```bash
$ cat hello.md # 'file.txt' 파일의 내용을 터미널 화면에 출력
hello codyssey
```

## 5. 🔐 권한 실습

`ls -l`을 입력하면 파일 정보가 한 줄씩 나열되는데, 보통 다음과 같은 형식을 가집니다.

> `-rw-r--r--  1 user  group  1234  Mar 31 14:00  example.txt`

---

### ## 각 항목의 의미 (왼쪽부터 순서대로)

| 항목 | 의미 | 설명 |
| :--- | :--- | :--- |
| **파일 유형 및 권한** | `-rw-r--r--` | 첫 글자는 유형(`-` 파일, `d` 디렉토리), 이후 9글자는 권한 |
| **링크 수** | `1` | 해당 파일/디렉토리에 연결된 하드 링크의 개수 |
| **소유자** | `user` | 파일을 생성한 사용자 계정 이름 |
| **그룹** | `group` | 파일이 속한 사용자 그룹 |
| **파일 크기** | `1234` | 파일의 용량 (기본 단위: 바이트) |
| **수정 시간** | `Mar 31 14:00` | 파일이 마지막으로 변경된 날짜와 시간 |
| **파일명** | `example.txt` | 파일이나 디렉토리의 실제 이름 |

---

### ### 💡 팁: 더 읽기 편하게 보려면?

기본 `ls -l`은 파일 크기가 바이트 단위라 읽기 불편할 때가 있죠. 그럴 땐 **`-h`** 옵션을 추가해 보세요.

* `ls -lh`: 크기를 KB, MB, GB 등 사람이 읽기 편한(Human-readable) 단위로 표시해 줍니다.
* `ls -lat`: 숨김 파일까지 포함(`-a`)하고, 시간순(`-t`)으로 정렬해서 보여줍니다.

---

### ### 권한(`-rw-r--r--`) 상세 분석
이 부분은 세 글자씩 끊어서 읽으면 쉽습니다.
1.  **첫 글자**: 타입 (`-`는 일반 파일, `d`는 디렉토리)
2.  **rw-**: **소유자**의 권한 (읽기, 쓰기 가능)
3.  **r--**: **그룹**의 권한 (읽기만 가능)
4.  **r--**: **기타 사용자**의 권한 (읽기만 가능)

혹시 특정 파일의 권한을 변경하는 방법(`chmod`)이나 소유자를 바꾸는 방법(`chown`)도 궁금하신가요? 원하시면 바로 알려드릴 수 있습니다!

### 📌 권한 확인

```bash
ls -l  # 파일 및 디렉토리의 상세 정보(권한, 소유자, 크기 등)를 목록 형태로 출력
```

### 📌 권한 변경

```bash
chmod 644 file.txt  # 'file.txt'의 권한을 644(rw-r--r--)로 변경하여 소유자만 쓰기 가능하게 설정
chmod 755 test-dir  # 'test-dir'의 권한을 755(rwxr-xr-x)로 변경하여 소유자만 쓰기/읽기/실행 가능, 나머지는 읽기/실행만 가능하게 설정
```

리눅스에서 그룹을 설정하고 관리하는 방법은 크게 세 가지 단계로 나뉩니다. **새 그룹 만들기**, **사용자를 그룹에 넣기**, 그리고 **파일의 그룹 바꾸기**입니다.

모든 설정은 시스템 관리자 권한이 필요하므로 명령어 앞에 `sudo`를 붙여야 합니다.

---

### ## 1. 새로운 그룹 만들기 (`groupadd`)
프로젝트팀이나 특정 부서를 위한 그룹을 새로 생성합니다.
* **명령어:** `sudo groupadd [그룹명]`
* **예시:** `sudo groupadd devteam` (devteam이라는 그룹 생성)

---

### ## 2. 사용자를 그룹에 추가하기 (`usermod`)
이미 존재하는 사용자(ID)를 방금 만든 그룹에 소속시킵니다.
* **명령어:** `sudo usermod -aG [그룹명] [사용자ID]`
    * `-a` (append): 기존 그룹 목록에 추가함
    * `-G` (groups): 추가할 그룹을 지정함
* **예시:** `sudo usermod -aG devteam alice` (alice를 devteam 그룹에 추가)

> **⚠️ 주의:** `-a` 옵션을 빠뜨리고 `-G`만 쓰면, 사용자가 기존에 속해 있던 다른 그룹에서 탈퇴될 수 있으니 꼭 `-aG`를 함께 쓰세요!

---

### ## 3. 파일의 소유 그룹 변경하기 (`chgrp`)
이제 특정 파일이나 디렉토리를 우리 그룹 멤버들이 공유할 수 있게 설정합니다.
* **명령어:** `sudo chgrp [그룹명] [파일명]`
* **예시:** `sudo chgrp devteam project.txt`
    * 이제 `ls -l`을 해보면 그룹 칸이 `devteam`으로 바뀐 것을 볼 수 있습니다.

---

### ## 4. 그룹 권한 부여하기 (`chmod`)
그룹을 설정했더라도 그룹 권한이 `---`(권한 없음)라면 소용이 없겠죠? 그룹 멤버들이 읽고 쓸 수 있게 권한을 줍니다.
* **명령어:** `chmod g+rw [파일명]` (그룹에게 읽기/쓰기 권한 추가)
* **결과 예시:** `-rw-rw-r--` (소유자와 그룹 모두 읽고 쓰기 가능)

---

### ### 💡 꿀팁: 지금 내 그룹 확인하기
내가 어떤 그룹들에 속해 있는지 궁금하다면 터미널에 바로 이 명령어를 쳐보세요.
* `groups`: 현재 내 계정이 속한 모든 그룹 나열
* `id`: 내 유저 ID(uid)와 그룹 ID(gid)를 상세히 확인

지금 바로 `groups`를 입력해서 본인이 어떤 그룹에 속해 있는지 확인해 보시겠어요? 결과가 어떻게 나오나요?

### 📊 변경 전/후 비교

```
(변경 전)
(변경 후)
```

### 📘 권한 설명

* r: read
* w: write
* x: execute

예:

* 755 → rwxr-xr-x
* 644 → rw-r--r--

---

## 6. 🐳 Docker 기본 실습
### 개요

**Docker**는 애플리케이션을 언제 어디서나 실행할 수 있도록 필요한 모든 요소(소스 코드, 라이브러리, 종속성 등)를 하나의 런타임 환경으로 패키징하는 **컨테이너 가상화 기술**입니다. 기존의 하드웨어 가상화와 달리 **운영체제(OS) 수준에서 가상화**를 수행하여 경량화된 격리 공간을 제공하는 것이 특징입니다.

Docker의 주요 개요와 핵심 개념은 다음과 같습니다.

### 1. 핵심 구성 요소
*   **컨테이너(Container):** 애플리케이션과 그 실행 환경을 하나로 묶은 **논리적인 격리 공간**입니다. 프로세스 수준의 속도로 빠르게 실행되며, 하나의 OS 위에서 여러 개의 컨테이너를 동시에 구동할 수 있습니다.
*   **이미지(Image):** 컨테이너를 실행하기 위한 **템플릿**으로, 애플리케이션 실행에 필요한 바이너리, 라이브러리, 설정 값 등을 포함합니다. 이미지는 상태를 가지지 않는 **Stateless** 구조이며, 여러 개의 불변(Immutable) 레이어로 구성됩니다.
*   **Dockerfile:** 이미지를 만들기 위한 **설계도** 역할을 하는 텍스트 파일입니다. 애플리케이션 설치 및 실행 스크립트를 포함하며, 이를 통해 어디서든 동일한 환경을 재현할 수 있습니다.

### 2. Docker의 동작 원리 (Workflow)
Docker는 일반적으로 다음과 같은 과정을 거쳐 애플리케이션을 배포합니다.
1.  **작성 (Dockerfile):** 애플리케이션 인프라 구성을 정의합니다.
2.  **빌드 (Build):** Dockerfile을 빌드하여 실행 가능한 **이미지**를 생성합니다.
3.  **공유 (Push/Pull):** 생성된 이미지를 **Docker Hub**와 같은 저장소(Registry)에 업로드하거나 다운로드합니다.
4.  **실행 (Run):** 이미지를 기반으로 **컨테이너**를 생성하고 서비스를 실행합니다.

### 3. 주요 장점
*   **높은 이식성:** 개인 PC, 클라우드 환경, 다양한 OS 등 Docker만 설치되어 있다면 **어떤 환경에서도 동일하게 동작**합니다.
*   **효율성 및 경량성:** OS 전체를 가상화하는 것이 아니라 프로세스 단위로 격리하기 때문에 시스템 리소스를 적게 사용하며 시작 속도가 매우 빠릅니다.
*   **확장 및 관리 용이:** 애플리케이션의 **확장(Scale-out)이 쉽고**, 컨테이너를 내리거나 삭제하는 관리 작업이 단순합니다.
*   **MSA(마이크로서비스 아키텍처) 적합:** 여러 계층의 서비스를 컨테이너로 분리하고 연결하여 실행하는 구조에 매우 유용합니다.

### 4. 사용 이유
Docker를 사용하면 개발 환경과 운영 환경의 불일치 문제를 해결할 수 있으며, 서버 세팅과 애플리케이션 배포 과정을 **반복 가능**하게 만들어 줍니다. 또한, 기업 내부의 보안이 중요한 이미지는 **Private Registry**를 구축하여 안전하게 관리할 수 있습니다.

Docker **이미지**와 **컨테이너**의 가장 큰 차이점은 **이미지는 '설계도(템플릿)'**이고, **컨테이너는 그 설계도를 바탕으로 실제로 '실행된 인스턴스'**라는 점입니다. 상세한 차이점은 다음과 같습니다.

### 1. 정의 및 성격
*   **Docker 이미지:** 애플리케이션 실행에 필요한 모든 요소(코드, 라이브러리, 종속성, 설정 등)를 포함하고 있는 **템플릿**입니다. 이미지는 여러 개의 **레이어(Layer)**로 구성되며, 컨테이너를 생성하기 위한 **정적인 파일** 묶음과 같습니다.
*   **Docker 컨테이너:** 이미지를 기반으로 실행되는 **격리된 프로세스**입니다. 이미지가 실제로 메모리에 적재되어 동작하는 **동적인 상태**를 의미하며, 하나의 이미지로부터 여러 개의 컨테이너를 동시에 생성하고 실행할 수 있습니다.

### 2. 불변성 (Stateless vs Stateful)
*   **이미지 (Stateless/Immutable):** 이미지는 **상태를 가지지 않으며(Stateless)**, 한 번 생성되면 **변경할 수 없는 불변(Immutable)** 구조입니다. 새로운 설정을 적용하려면 기존 이미지를 수정하는 것이 아니라 새로운 이미지를 다시 빌드해야 합니다.
*   **컨테이너 (휘발성):** 컨테이너는 실행 중에 데이터를 읽고 쓸 수 있지만, 기본적으로 **휘발성**을 가집니다. 컨테이너가 삭제되면 실행 중에 변경되거나 저장된 데이터도 함께 사라지기 때문에, 데이터를 보존하려면 볼륨(Volume)이나 마운트(Mount)를 사용하여 외부 저장소에 연결해야 합니다.

### 3. 워크플로우와 실행 관계
*   **관계:** `Dockerfile`을 빌드하면 **이미지**가 생성되고, 그 이미지를 실행(`run`)하면 **컨테이너**가 됩니다.
*   **비유:** 이미지를 **운영체제 설치 파일(ISO)**에 비유한다면, 컨테이너는 그 파일을 사용하여 **컴퓨터에 운영체제를 설치하고 구동 중인 상태**에 비유할 수 있습니다.

### 4. 구조적 차이 요약
| 구분 | Docker 이미지 | Docker 컨테이너 |
| :--- | :--- | :--- |
| **역할** | 컨테이너를 생성하기 위한 설계도/템플릿 | 이미지가 실행된 실제 런타임 환경 |
| **상태** | **Stateless**, 불변(Immutable) 레이어 구조 | 이미지 위에 쓰기 가능한 레이어가 추가된 상태 |
| **수명** | 삭제하기 전까지 영구적으로 저장됨 | 생성, 실행, 중지, 삭제 등 생명주기를 가짐 |
| **구성 요소** | 바이너리, 라이브러리, 설정 값 등 | 실행 중인 프로세스 및 격리된 시스템 자원 |
### 📌 hello-world 실행

```bash
Last login: Fri Apr  3 21:22:13 on console
mpeg46551@c5r1s2 ~ % docker -v 
Docker version 28.5.2, build ecc6942

mpeg46551@c5r1s2 ~ % docker run hello-world # 'hello-world' 이미지를 다운로드하고 컨테이너로 실행하여 정상 작동 확인
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest

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
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

mpeg46551@c5r1s2 ~ % docker  ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                          PORTS     NAMES
c9c920c75fc0   hello-world   "/hello"   About a minute ago   Exited (0) About a minute ago             friendly_yalow
```

👉 결과:
Docker 전문가로서 `hello-world` 실행 과정과 컨테이너 상태에 대해 상세히 설명해 드리겠습니다.

### 1. `docker run hello-world` 실행 과정 상세 분석
사용자가 입력한 명령어가 처리된 과정은 다음과 같습니다:

1.  **로컬 이미지 확인**: Docker 클라이언트가 로컬 저장소에서 `hello-world:latest` 이미지를 찾습니다. [cite_start]`Unable to find image... locally` 메시지는 로컬에 해당 이미지가 없음을 의미합니다[cite: 5].
2.  [cite_start]**이미지 다운로드 (Pull)**: 로컬에 이미지가 없으므로 Docker 데몬이 온라인 저장소인 **Docker Hub**에서 해당 이미지를 자동으로 다운로드(Pull)합니다[cite: 5, 12].
3.  [cite_start]**컨테이너 생성 및 실행**: 다운로드가 완료되면 해당 이미지를 기반으로 격리된 프로세스인 **컨테이너**를 생성하고 실행합니다[cite: 19, 31].
4.  [cite_start]**결과 출력**: 컨테이너 내부의 실행 파일이 "Hello from Docker!"라는 메시지를 생성하여 터미널에 출력합니다[cite: 5].

### 2. 왜 `ps` 검사 시 `Exited (0)`로 나오나요?
`docker ps -a` 결과에서 상태가 `Exited (0)`인 이유는 컨테이너의 **설계 목적** 때문입니다.

* [cite_start]**단일 애플리케이션 실행**: 컨테이너는 특정 작업(애플리케이션 실행)을 위해 패키징된 프로세스입니다[cite: 13, 18].
* **작업 완료 후 종료**: `hello-world` 컨테이너는 화면에 안내 메시지를 출력하는 것이 유일한 임무입니다. [cite_start]메시지 출력을 마치면 컨테이너 내부의 메인 프로세스가 종료되므로, 컨테이너 자체도 자동으로 종료 상태가 됩니다[cite: 18].
* **상태 코드 (0)**: `Exited (0)`에서 `0`은 프로세스가 에러 없이 **정상적으로 종료**되었음을 의미합니다.

### 3. 주요 관련 명령어 팁
* [cite_start]**실행 중인 컨테이너 확인**: `docker ps` (종료된 컨테이너는 보이지 않음) [cite: 12, 19]
* [cite_start]**모든 컨테이너 확인**: `docker ps -a` (종료된 컨테이너를 포함하여 전체 목록 확인) [cite: 12]
* [cite_start]**이미지 목록 확인**: `docker images` (다운로드된 `hello-world` 이미지를 확인할 수 있음) [cite: 19]

결론적으로, 사용자의 실행 결과는 **지극히 정상**입니다. Docker가 제대로 설치되었고, 외부 저장소에서 이미지를 가져와 실행하는 전체 워크플로우가 완벽하게 작동하고 있음을 보여줍니다. [cite_start]이제 안내 메시지에 나온 대로 `docker run -it ubuntu bash`와 같은 명령어를 통해 더 복잡한 환경을 실습해 보시는 것을 추천합니다[cite: 5].

전문가적인 시각에서 답변해 드릴게요. 이미 `hello-world` 컨테이너가 `Exited` 상태로 남아있는 상황에서 **다시 `docker run hello-world`를 실행하면 다음과 같은 일이 벌어집니다.**

### 1. 결론: 새로운 컨테이너가 하나 더 생깁니다
Docker의 `run` 명령어는 **"이미지를 가지고 새로운 컨테이너를 만들어서 실행해라"**라는 뜻입니다. 따라서 기존에 죽어있는(Exited) 컨테이너를 다시 쓰는 게 아니라, **똑같은 이미지로 만든 '새로운 컨테이너'가 하나 더 추가**됩니다.

### 2. 실행 후 `docker ps -a`를 확인하면?
명령어를 다시 실행한 후 목록을 확인해 보시면 아래와 같이 보일 겁니다.
* **기존 컨테이너**: `Exited (0)` 상태 (이전 기록)
* **새로운 컨테이너**: `Exited (0)` 상태 (방금 실행된 기록)

즉, 실행할 때마다 컨테이너 ID가 다른 별개의 인스턴스가 계속 생성되어 목록에 쌓이게 됩니다.

---

### 3. 실무형 관리 팁 💡

만약 "나는 목록이 지저분해지는 게 싫고, 딱 한 번만 실행하고 바로 지워졌으면 좋겠다" 하신다면 아래 옵션을 기억하세요.

* **자동 삭제 옵션 (`--rm`)**:
    실행이 끝나자마자 컨테이너를 목록에서 자동으로 삭제해 줍니다. 연습할 때 아주 유용합니다.
    ```bash
    docker run --rm hello-world
    ```

* **기존 컨테이너 재시작 (`start`)**:
    새로 만들지 않고 이미 죽어있는 그 컨테이너를 다시 살리고 싶다면 `run`이 아니라 `start`를 씁니다. (단, `hello-world`는 메시지만 뿌리고 바로 종료되므로 `start -a`를 써야 결과를 볼 수 있습니다.)
    ```bash
    docker start -a <컨테이너_ID>
    ```

* **청소하기**:
    종료된 컨테이너들이 너무 많아졌다면 한 번에 싹 지울 수 있습니다.
    ```bash
    docker container prune
    ```

**요약하자면:** `run`을 계속하면 실행한 횟수만큼 컨테이너 쓰레기(?)가 쌓이게 되니, 테스트용이라면 `--rm` 옵션을 습관화하시는 것이 좋습니다! 다음 단계로 넘어가 볼까요? 어떤 이미지를 더 실행해보고 싶으신가요?
```
(출력 결과)
```
sdfㄴㅇㄹㅇㄴ ㄹㅇㄹㄴㅇds
---
sdfㄴㅇㄹㅇㄴ ㄹㅇㄹㄴㅇds
### 📌 Ubuntu 컨테이너 실행

```bash
docker run -it ubuntu bash  # 'ubuntu' 이미지를 기반으로 컨테이너를 실행하고 대화형 bash 셸 환경으로 진입
```

```bash
ls  # 컨테이너 내부의 현재 디렉토리 목록 확인 (파일 및 디렉토리 출력)
echo hello  # 터미널 화면에 'hello'라는 문자열 출력
```

---

### 📌 컨테이너 상태 확인

```bash
docker ps  # 현재 실행 중인 Docker 컨테이너 목록 확인
docker ps -a  # 종료된 컨테이너를 포함한 모든 Docker 컨테이너 목록 확인
docker images  # 로컬 시스템에 저장된 Docker 이미지 목록 확인
```

---

### 📌 로그 및 리소스 확인

```bash
docker logs <컨테이너>  # 지정한 컨테이너 내부에서 발생한 표준 출력(로그) 확인
docker stats  # 실행 중인 컨테이너들의 실시간 리소스(CPU, 메모리 등) 사용량 확인
```

---

## 7. 🏗️ Dockerfile 기반 웹 서버

### 📁 폴더 구조

```
project/
 ├── Dockerfile
 └── site/
     └── index.html
```

---

### 📄 Dockerfile

```dockerfile
FROM nginx:alpine
COPY site/ /usr/share/nginx/html/
```

---

### 📄 index.html

```html
<h1>Hello DevOps</h1>
```

---

### ⚙️ 이미지 빌드

```bash
docker build -t my-web .  # 현재 디렉토리(.)의 Dockerfile을 사용하여 'my-web'이라는 이름(태그)의 이미지 빌드
```

---

### 🚀 컨테이너 실행

```bash
docker run -d -p 8080:80 --name my-web my-web  # 'my-web' 이미지를 백그라운드(-d)에서 실행하며, 호스트 8080 포트를 컨테이너 80 포트에 매핑(-p)하고 이름 지어 실행
```

---

### 🌐 접속 확인

```
http://localhost:8080
```

📸 (스크린샷 첨부)

---

## 8. 🌐 포트 매핑 설명

포트 매핑은 호스트와 컨테이너를 연결하기 위해 필요하다.

* 컨테이너 내부는 외부에서 직접 접근 불가능
* `-p 8080:80` → 호스트 8080 → 컨테이너 80 연결

---

## 9. 📦 바인드 마운트

```bash
docker run -d -p 8080:80 \
-v $(pwd)/site:/usr/share/nginx/html \
nginx  # 백그라운드 실행(-d), 포트 매핑(-p), 로컬 site 디렉토리를 컨테이너에 바인드 마운트(-v)
```

### 🔍 변경 확인

1. index.html 수정
2. 브라우저 새로고침

👉 결과: 즉시 반영됨

📸 (변경 전/후 캡처)

---

## 10. 💾 Docker 볼륨 (영속성)

### 📌 볼륨 생성

```bash
docker volume create mydata  # 'mydata'라는 이름의 Docker 관리를 받는 볼륨 생성
```

---

### 📌 데이터 저장

```bash
docker run -it -v mydata:/data ubuntu bash  # 'mydata' 볼륨을 컨테이너 내부의 '/data' 경로에 마운트하여 ubuntu 대화형 셸 실행
```

```bash
echo hello > /data/test.txt  # '/data' 폴더 내에 'test.txt' 파일을 생성하고 'hello' 텍스트를 기록 (볼륨에 데이터 저장)
exit  # 컨테이너 종료 및 빠져나오기
```

---

### 📌 컨테이너 삭제 후 확인

```bash
docker run -it -v mydata:/data ubuntu bash  # 동일한 'mydata' 볼륨을 연결하여 새로운 ubuntu 컨테이너 다시 실행
cat /data/test.txt  # 이전 컨테이너에서 만들어둔 'test.txt' 파일의 내용을 출력하여 데이터 보존 확인
```

👉 결과: 데이터 유지됨

---

## 11. 🔄 바인드 마운트 vs 볼륨

| 항목 | 바인드 마운트  | 볼륨        |
| -- | -------- | --------- |
| 위치 | 호스트 디렉토리 | Docker 관리 |
| 반영 | 즉시 반영    | 내부 저장     |
| 용도 | 개발       | 데이터 저장    |

---

## 12. 🔧 Git 설정

```bash
git config --global user.name "이름"  # Git 커밋에 사용할 전역(global) 사용자 이름 설정
git config --global user.email "이메일"  # Git 커밋에 사용할 전역(global) 사용자 이메일 설정
git config --list  # 현재 설정된 Git 환경설정 전체 목록 출력 확인
```

📸 (결과 캡처)

---

## 13. 🔗 GitHub 연동

### 1. Git 환경 설정 및 초기화 (git init부터)
그전에 사용자 정보 등록

* [cite_start]**사용자 정보 설정**: 커밋(기록)을 남길 때 누가 작성했는지 식별하기 위해 이름과 이메일을 먼저 설정해야 합니다. [cite: 1176]
```bash
    > git config --global user.name "mpegdj"
    > git config --global user.email "mpeg4@ymail.com"
    > git config --global -l 
        user.name=mpegdj
        user.email=mpeg4@ymail.com
```

* **저장소 초기화 (`git init`)**: 프로젝트 루트 폴더에서 이 명령어를 실행하면 해당 디렉토리가 Git 저장소로 관리되기 시작합니다. 
* **기본 파일 생성**: 프로젝트에 대한 설명이 담긴 `README.md`와 Git 관리에서 제외할 파일을 지정하는 `.gitignore` 파일을 생성하는 것이 관례입니다. 
* **첫 커밋**: 파일을 생성한 후 `git add .` 명령어로 상태를 추적하고, `git commit -m "Initial commit"`으로 첫 기록을 남깁니다. 

### 2. 리눅스에서 Docker 활용하기
[cite_start]Docker는 애플리케이션과 그에 필요한 모든 종속 항목을 하나로 묶어 '컨테이너'라는 격리된 환경에서 실행하게 해줍니다. [cite: 555, 560]

* [cite_start]**Docker 실행 환경 (OrbStack 등)**: 리눅스 환경에서 보안 정책상 직접적인 `sudo` 권한 사용이 제한될 경우, OrbStack과 같은 도구를 사용하여 Docker 엔진을 구동할 수 있습니다. [cite: 564, 567]
* **핵심 활용 흐름**:
    1.  [cite_start]**Dockerfile 작성**: 애플리케이션 실행에 필요한 베이스 이미지, 파일 복사(`COPY`), 작업 디렉토리 설정(`WORKDIR`), 실행 명령(`CMD`) 등을 정의합니다. [cite: 1802, 1819]
    2.  [cite_start]**이미지 빌드**: 작성한 Dockerfile을 기반으로 실행 가능한 이미지를 만듭니다. [cite: 1815]
    3.  [cite_start]**컨테이너 실행**: 빌드된 이미지를 `docker run` 명령어로 실행하며, 이때 외부에서 접속할 수 있도록 포트 매핑(`-p`) 설정을 함께 합니다. [cite: 558, 1541]
* [cite_start]**데이터 영속성 관리**: 컨테이너가 삭제되어도 데이터가 사라지지 않도록 '볼륨(Volume)'이나 '바인드 마운트(Bind Mount)'를 설정하여 데이터를 호스트 시스템에 저장하고 관리합니다. [cite: 558, 1612]

[cite_start]**전문가 팁**: Git으로 소스 코드를 관리하고, 그 소스 코드를 Docker로 컨테이너화하여 실행하는 방식은 "내 컴퓨터에서는 되는데 서버에서는 안 돼요"라는 문제를 해결하는 현대 개발의 표준 기반입니다. [cite: 554, 556] 

Git 초기 설정을 마친 후, 간단한 Dockerfile을 작성해 보시는 것을 추천합니다. 무엇을 먼저 해보시겠어요?
* 저장소 생성
* VSCode 로그인
* push 완료

📸 (스크린샷 첨부)

---

## 14. 🚨 트러블슈팅

### ❗ 문제 1: Docker 실행 안됨

* 원인:
* 해결:

---

### ❗ 문제 2: 포트 접속 안됨

* 원인:
* 해결:

---

## 15. 📚 핵심 개념 정리

### 📌 절대 경로 vs 상대 경로

* 절대 경로: `/home/user/file.txt`
* 상대 경로: `./file.txt`

---

### 📌 포트 매핑이 필요한 이유

* 컨테이너는 외부에서 직접 접근 불가
* 호스트와 연결 필요

---

### 📌 Docker 볼륨

* 컨테이너 삭제 후에도 데이터 유지

---

### 📌 Git vs GitHub

* Git: 로컬 버전 관리
* GitHub: 원격 저장소 및 협업 플랫폼

---

# ✅ 완료

README만으로 전체 과정 재현 가능하도록 작성 완료.

---

# 🔥 사용 팁 (중요)

* ❌ “설명만 쓰기” → 탈락
* ✅ “명령어 + 결과 + 캡처” → 합격

---

원하면 다음으로
👉 **트러블슈팅 2개 실제로 쓸만한 거 같이 만들어줄게**
