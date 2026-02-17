# Beats

## Beats의 종류

1. Filebeat(파일비트)

- 아래와 같은 유형의 시스템, 어플리케이션의 로그를 수집
    - 디스크에 있는 파일
    - HTTP API 엔드포인트
    - MQ 종류의 메시지 스트림
    - Syslog 리스터

2. Metricbeat(메트릭비트)

- 다양한 시스템, 프로토콜에서 시스템과 어플리케이션, 플랫폼의 메트릭을 수집

3. Auditbeat(오딧비트)

- 프레임워크에서 규정한 운영체제 감사 데이터 수집

4. Heartbeat(하트비트)

- iCMP, TCP, HTTP 프로토콜을 통해 어플리케이션과 서비스 가동 시간과 가용성 정보를 수집하고 모니터링

5. Packetbeat(패킷비트)

- 분석 대상 호스트에서 실시간으로 네트워크패킷 정보를 수집하고 복호화(decode)함
- 모든 통신에 대해 네트워크 트래픽 정보를 탐지하거나 시스템 활동 상태에 대해 더 깊은 통찰력을 얻기 위해 특정 프로토콜을 선택해 분석에 적덜할 형태로 변환

6. Winlogbeat(윈로그비트)

- 윈도우 시스템에서 발생하는 이벤트 로그를 수집

7. Functionbeat(펑션비트)

- 클라우드용 로그 소스에서 데이터를 수집

<br />

---

<br />

## Beats 사용 예제

### 파일비트를 이용한 로그 수집

- 모듈 활성화

```sh
# nginx 모듈 활성화
filebeat modules enable nginx

# 혹은
/path/to/filebeat modules enable nginx
```

- 설정파일 수정

```yml
# ============================== Filebeat modules ==============================

filebeat.config.modules:
  # Glob pattern for configuration loading
  path: ${path.config}/modules.d/*.yml

# ---------------------------- Elasticsearch Output ----------------------------
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["localhost:9200"]

  # Protocol - either `http` (default) or `https`.
  protocol: "https"
  ssl.certificate_authorities: ["/path/to/config/certs/http_ca.crt"]

  username: "elastic"
  password: "changeme"

# ================================= Processors =================================

processors:
  - add_host_metadata: ~
  - add_cloud_metadata: ~
```

```sh
/path/to/filebeat setup -E "setup.kibana.host=localhost:5601" -M "nginx.access.enabled=true" -M "nginx.error.enabled=true" --dashboards --pipelines

## 성공시 반환
# Loading dashboards (Kibana must be running and reachable)
# Loaded dashboards
# Loaded Ingest pipelines

```

- 구동

```sh
systemctl start filebeat

# 혹은

/path/to/.filebeat
```