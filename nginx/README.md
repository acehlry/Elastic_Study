# Nginx 다운로드

```sh
# 최신 안정 버전 확인
curl -I https://nginx.org/download/

# Response
#
# HTTP/1.1 200 OK
# Server: nginx/1.29.3
# Date: Tue, 17 Feb 2026 07:19:52 GMT
# Content-Type: text/html; charset=utf-8
# Connection: keep-alive
# Keep-Alive: timeout=15
# Strict-Transport-Security: max-age=31536000
```

```sh
# nginx 다운로드
wget https://nginx.org/download/nginx-1.29.3.tar.gz

# 압축해제
tar -xvzf nginx-1.29.3.tar.gz
```

```sh
# nginx 빌드
path/configure

# 빌드 경로지정
path/configure --prefix=/usr/local/nginx

# 컴파일
make

# 빌드 결과물 설치
sudo make install

## 안될 경우 컴파일러 설치

# 설치
sudo apt install build-essential
# 버전 확인
gcc --version

# 그래도 안될 경우 nginx 필수 빌드 라이브러리 설치
sudo apt install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev
```