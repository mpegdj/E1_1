# 1. 베이스 이미지 선택 (Nginx 사용 예시)
FROM nginx:latest

# 2. 호스트의 app 폴더 안의 내용을 컨테이너의 nginx 경로로 복사
# (현재 위치가 프로젝트 루트이므로 ./app/ 경로를 사용합니다)
COPY ./app/ /usr/share/nginx/html/

# 3. 80번 포트 개방 알림
EXPOSE 80