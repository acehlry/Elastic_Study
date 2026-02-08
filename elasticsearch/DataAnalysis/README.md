# 데이터 분석

## 집계

- 메트릭 집계(Metric aggregation)는 숫자 데이터에 대한 개수, 합계, 최솟값, 최댓값, 평균 같은 메트릭을 계산
- 버킷 집계(Bucket aggregation)는 대규모 데이터 세트를 필드의 값에 따라 그룹화한다. 범위, 날짜, 검색 결과(또는 코퍼스) 내 텀의 빈도수 등을 기반으로 버킷을 만듬

### 집계의 사용처

- 키바나의 시각화, 대시보드, 솔루션별 어플리케이션
- 지도 및 비지도 머신러닝 작업
- 엔티티 중심 인덱스의 변환 작업

## 예제

1. 해당 기간에 생서오딘 모드 로그 검색

- size=0으로 설정하여 검색 요청에 대해 개별 문서를 반환하지 않음, 대용량 데이터 세트를 분석

```json
GET web-logs/_search?size=0
{
    "query": {
        "range": {
            "@timestamp": {
                "gte": "2019-01-23T00:00:00.000Z",
                "lt": "2019-01-24T00:00:00.000Z"
            }
        }
    }
}

// Response
{
  "took" : 37,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 4654,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  }
}
```

2. 지정한 기간에 웹 서버가 제공한 바이트 수를 나타내는 메트릭을 계산

```json
GET web-logs/_search?size=0
{
  "query": {
    "range": {
      "@timestamp": {
        "gte": "2019-01-23T00:00:00.000Z",
        "lt": "2019-01-24T00:00:00.000Z"
      }
    }
  },
  "aggs": {
    "bytes_served": {
      "sum": {
        "field": "http.response.body.bytes",
      }
    }
  }
}

// Response
{
  "took" : 8,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 4654,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "bytes_served" : {
      "value" : 5.8785836E7
    }
  }
}
```

3. 모든 로그를 그룹화하기보다는 데이터를 시간별로 묶어 세분화

- 집계를 상위 집계 내에 중첩

```json
GET web-logs/_search?size=0
{
  "query": {
    "range": {
        "@timestamp": {
          "gte": "2019-01-23T00:00:00.000Z",
          "lt": "2019-01-24T00:00:00.000Z"
        }
      }
  },
  "aggs": {
    "hourly": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      },
      "aggs": {
        "bytes_served": {
          "sum": { "field": "http.response.body.bytes" }
        }
      }
    }
  }
}
```

4. 계절성 패턴을 확인하기 위해 기간을 2일로 늘림, 바이트를 킬로바이트로 변환

```json
GET web-logs/_search?size=0
{
  "query": {
    "range": {
        "@timestamp": {
          "gte": "2019-01-23T00:00:00.000Z",
          "lt": "2019-01-24T00:00:00.000Z"
        }
      }
  },
  "aggs": {
    "hourly": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      },
      "aggs": {
        "bytes_served": {
          "sum": {
              "field": "http.response.body.bytes",
              "script": {"source": "_value/(1024)"}
          }
        }
      }
    }
  }
}
```
