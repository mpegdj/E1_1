
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
| OS       | (예: macOS / Windows / Ubuntu)  |
| Shell    | (예: bash / zsh)                |
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

```
(출력 결과 붙여넣기)
```

---

### 📄 파일 내용 확인

```bash
cat file.txt  # 'file.txt' 파일의 내용을 터미널 화면에 출력
```

---

## 5. 🔐 권한 실습

### 📌 권한 확인

```bash
ls -l  # 파일 및 디렉토리의 상세 정보(권한, 소유자, 크기 등)를 목록 형태로 출력
```

### 📌 권한 변경

```bash
chmod 644 file.txt  # 'file.txt'의 권한을 644(rw-r--r--)로 변경하여 소유자만 쓰기 가능하게 설정
chmod 755 test-dir  # 'test-dir'의 권한을 755(rwxr-xr-x)로 변경하여 소유자만 쓰기/읽기/실행 가능, 나머지는 읽기/실행만 가능하게 설정
```

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

### 📌 hello-world 실행

```bash
docker run hello-world  # 'hello-world' 이미지를 다운로드하고 컨테이너로 실행하여 정상 작동 확인
```

👉 결과:

```
(출력 결과)
```

---

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
