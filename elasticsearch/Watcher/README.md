# Watcher(워처)

<br />

수신 데이터에 대한 자동 경보와 대응 조치를 제공 (단, 유료 구독 서비스임)

<br />

## Use Case

- `특정 값에서 발생하는 단일 이벤트`에 대한 경보

```
event.serverity: critical일 때
disk_free < 16B 일 때
```

- `필터와 일치하는 이벤트 개수가 임계치를 초과`하는 경우에 대한 경보

```
최근 5분 동안 event.severity: critical인 이벤트가 10개 이상인 경우
최근 5분 동안 username당 login_failed 이벤트 개수가 5개 이상인 경우
```

- `메트릭 집계 값이 특정 임계치를 초과`하는 경우

```
최근 5분 동안 평균 cpu.usage가 70%를 초과하는 경우
```

<br />

## Watcher의 수행

- 시간 간격에 따라 워처 경보를 작동 및 실행
- 엘라스틱서치 인덱스와 HTTP API 요청에서 입력 데이터를 가져옴, 경보 콘텍스트 내에서 다양한 입력을 지원
- 조건부 논리와 비교해서 입력 데이터를 평가해서 작업을 실행해야 하는지 결정
- 선택적으로 입력 데이터를 변환하고 작업을 실행
- 이메일 보내기, 웹훅(webhook) 요청 실행, 엘라스틱 서치 인덱스로 문서 색인(조건이 true로 평가되는 경우)과 같은 작업을 실행해 데이터에 응답

<br />

## Watcher 예제

```json
PUT _watcher/watch/test-watch
{
    "trigger": { "schedule": { "interval": "5m" }},
    "input": {
        "simple": {
            "run_action": true
        }
    },
    "transform": {
        "script": "return [ 'action_result' : 'Action executed' ]"
    },
    "actions": {
        "write_to_index": {
            "index": {
                "index": "test-watcher-alerts"
            }
        }
    }
}
```