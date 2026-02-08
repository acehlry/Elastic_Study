# 엘라스틱 서치

## 데이터 검색

로그 스태시를 통해 데이터 입력

```conf
input {
    stdin {}
}

filter {
  mutate {
    remove_field => ["host", "@version"]
  }
}

output {
  stdout {
    codec => dots {}
  }

  elasticsearch {
    hosts => "https://localhost:9200"
    user => "elastic"
    password => "6XU9t8-Ja68s_eJqeF8*"
    index => "web-logs"
    pipeline => "web-logs"
    ssl => true
    cacert => "/home/char1ey/workspace/13.LOG_MONITORING/elasticsearch-8.0.1/config/certs/http_ca.crt"
  }
}
```

```sh
/path/to/bin/logstash -f ./config/web-logs-logstash.conf < web.log --path.settings ./logstash
```

```json
GET web-logs/_count
// Response
{
  "count" : 20730,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  }
}

GET web-logs/_search

// Response
{
  "took" : 4,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 10000,
      "relation" : "gte"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "web-logs",
        "_id" : "TVEbPZwBB-P0iF0O5el5",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 44244,
              "organization" : {
                "name" : "Iran Cell Service and Communication Company"
              }
            },
            "address" : "5.124.121.10",
            "ip" : "5.124.121.10"
          },
          "url" : {
            "original" : "/image/6079/productModel/100x100"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T13:33:02.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/browse/digital-supplies/%D9%84%D9%88%D8%A7%D8%B2%D9%85-%D8%AF%DB%8C%D8%AC%DB%8C%D8%AA%D8%A7%D9%84",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 2498
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.237088042Z",
            "original" : "5.124.121.10 - - [26/Jan/2019:17:03:02 +0330] \\\"GET /image/6079/productModel/100x100 HTTP/1.1\\\" 200 2498 \\\"https://www.zanbil.ir/browse/digital-supplies/%D9%84%D9%88%D8%A7%D8%B2%D9%85-%D8%AF%DB%8C%D8%AC%DB%8C%D8%AA%D8%A7%D9%84\\\" \\\"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.941302Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0",
            "os" : {
              "name" : "Windows",
              "version" : "10",
              "full" : "Windows 10"
            },
            "name" : "Firefox",
            "device" : {
              "name" : "Other"
            },
            "version" : "64.0."
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "EFEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 31549,
              "organization" : {
                "name" : "Aria Shatel PJSC"
              }
            },
            "address" : "151.239.135.192",
            "ip" : "151.239.135.192"
          },
          "url" : {
            "original" : "/image/8882/specialSale"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:52:30.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 36269
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.320678782Z",
            "original" : "151.239.135.192 - - [26/Jan/2019:16:22:30 +0330] \\\"GET /image/8882/specialSale HTTP/1.1\\\" 200 36269 \\\"https://www.zanbil.ir/\\\" \\\"Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894371Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "7",
              "full" : "Windows 7"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "EVEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 58224,
              "organization" : {
                "name" : "Iran Telecommunication Company PJS"
              }
            },
            "address" : "89.38.198.45",
            "ip" : "89.38.198.45"
          },
          "url" : {
            "original" : "/static/images/amp/blog.png"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:52:42.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/filter/p65%2Cb1%2Cstexists",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 3863
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.320904963Z",
            "original" : "89.38.198.45 - - [26/Jan/2019:16:22:42 +0330] \\\"GET /static/images/amp/blog.png HTTP/1.1\\\" 200 3863 \\\"https://www.zanbil.ir/filter/p65%2Cb1%2Cstexists\\\" \\\"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894385Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0",
            "os" : {
              "name" : "Windows",
              "version" : "10",
              "full" : "Windows 10"
            },
            "name" : "Firefox",
            "device" : {
              "name" : "Other"
            },
            "version" : "64.0."
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "ElEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 31549,
              "organization" : {
                "name" : "Aria Shatel PJSC"
              }
            },
            "address" : "151.239.236.46",
            "ip" : "151.239.236.46"
          },
          "url" : {
            "original" : "/image/get?path=/Image/1(13).jpg"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:52:50.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/product/247/58783/%DB%8C%D8%AE%DA%86%D8%A7%D9%84-%D9%81%D8%B1%DB%8C%D8%B2%D8%B1-%D8%B3%D8%A7%DB%8C%D8%AF-%D8%A8%D8%A7%DB%8C-%D8%B3%D8%A7%DB%8C%D8%AF-%D8%B3%D8%A7%D9%85%D8%B3%D9%88%D9%86%DA%AF-%D9%85%D8%AF%D9%84-Polaris-W",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 53316
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.321194784Z",
            "original" : "151.239.236.46 - - [26/Jan/2019:16:22:50 +0330] \\\"GET /image/get?path=/Image/1(13).jpg HTTP/1.1\\\" 200 53316 \\\"https://www.zanbil.ir/product/247/58783/%DB%8C%D8%AE%DA%86%D8%A7%D9%84-%D9%81%D8%B1%DB%8C%D8%B2%D8%B1-%D8%B3%D8%A7%DB%8C%D8%AF-%D8%A8%D8%A7%DB%8C-%D8%B3%D8%A7%DB%8C%D8%AF-%D8%B3%D8%A7%D9%85%D8%B3%D9%88%D9%86%DA%AF-%D9%85%D8%AF%D9%84-Polaris-W\\\" \\\"Mozilla/5.0 (Windows NT 6.2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894391Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "8",
              "full" : "Windows 8"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "E1EbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "region_iso_code" : "IR-23",
              "city_name" : "Tehran",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "region_name" : "Tehran",
              "location" : {
                "lon" : 51.4158,
                "lat" : 35.6824
              }
            },
            "as" : {
              "number" : 44244,
              "organization" : {
                "name" : "Iran Cell Service and Communication Company"
              }
            },
            "address" : "5.116.129.70",
            "ip" : "5.116.129.70"
          },
          "url" : {
            "original" : "/static/images/arrow-left.png"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:52:58.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://znbl.ir/static/bundle-bundle_site_head.css",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 474
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.322246977Z",
            "original" : "5.116.129.70 - - [26/Jan/2019:16:22:58 +0330] \\\"GET /static/images/arrow-left.png HTTP/1.1\\\" 200 474 \\\"https://znbl.ir/static/bundle-bundle_site_head.css\\\" \\\"Mozilla/5.0 (Windows NT 6.3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894403Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "8.1",
              "full" : "Windows 8.1"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "FFEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 58224,
              "organization" : {
                "name" : "Iran Telecommunication Company PJS"
              }
            },
            "address" : "91.250.233.74",
            "ip" : "91.250.233.74"
          },
          "url" : {
            "original" : "/image/63274/productModel/150x150"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:53:06.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/browse/digital-camera/%D8%AF%D9%88%D8%B1%D8%A8%DB%8C%D9%86-%D8%B9%DA%A9%D8%A7%D8%B3%DB%8C",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 5317
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.322581206Z",
            "original" : "91.250.233.74 - - [26/Jan/2019:16:23:06 +0330] \\\"GET /image/63274/productModel/150x150 HTTP/1.1\\\" 200 5317 \\\"https://www.zanbil.ir/browse/digital-camera/%D8%AF%D9%88%D8%B1%D8%A8%DB%8C%D9%86-%D8%B9%DA%A9%D8%A7%D8%B3%DB%8C\\\" \\\"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894408Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "7",
              "full" : "Windows 7"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "FVEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 58224,
              "organization" : {
                "name" : "Iran Telecommunication Company PJS"
              }
            },
            "address" : "2.178.168.11",
            "ip" : "2.178.168.11"
          },
          "url" : {
            "original" : "/static/css/font/wyekan/font.woff"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:53:15.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://znbl.ir/static/bundle-bundle_site_head.css",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 28536
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.322852329Z",
            "original" : "2.178.168.11 - - [26/Jan/2019:16:23:15 +0330] \\\"GET /static/css/font/wyekan/font.woff HTTP/1.1\\\" 200 28536 \\\"https://znbl.ir/static/bundle-bundle_site_head.css\\\" \\\"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894414Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "7",
              "full" : "Windows 7"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "FlEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 44244,
              "organization" : {
                "name" : "Iran Cell Service and Communication Company"
              }
            },
            "address" : "5.115.251.228",
            "ip" : "5.115.251.228"
          },
          "url" : {
            "original" : "/image/56356/productModel/200x200"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:53:26.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/m/filter/b43%2Cp63%2Ct40",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 8393
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.323096515Z",
            "original" : "5.115.251.228 - - [26/Jan/2019:16:23:26 +0330] \\\"GET /image/56356/productModel/200x200 HTTP/1.1\\\" 200 8393 \\\"https://www.zanbil.ir/m/filter/b43%2Cp63%2Ct40\\\" \\\"Mozilla/5.0 (Linux; Android 8.0.0; SAMSUNG SM-J600F Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/7.0 Chrome/59.0.3071.125 Mobile Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894420Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Linux; Android 8.0.0; SAMSUNG SM-J600F Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/7.0 Chrome/59.0.3071.125 Mobile Safari/537.36",
            "os" : {
              "name" : "Android",
              "version" : "8.0.0",
              "full" : "Android 8.0.0"
            },
            "name" : "Samsung Internet",
            "device" : {
              "name" : "Samsung $2"
            },
            "version" : "7.0"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "F1EbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Asia",
              "country_iso_code" : "IR",
              "country_name" : "Iran",
              "location" : {
                "lon" : 51.4115,
                "lat" : 35.698
              }
            },
            "as" : {
              "number" : 31549,
              "organization" : {
                "name" : "Aria Shatel PJSC"
              }
            },
            "address" : "151.239.135.192",
            "ip" : "151.239.135.192"
          },
          "url" : {
            "original" : "/image/153/brand"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:53:33.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/browse/home-appliances/%D9%84%D9%88%D8%A7%D8%B2%D9%85-%D8%AE%D8%A7%D9%86%DA%AF%DB%8C",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 2566
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.325824471Z",
            "original" : "151.239.135.192 - - [26/Jan/2019:16:23:33 +0330] \\\"GET /image/153/brand HTTP/1.1\\\" 200 2566 \\\"https://www.zanbil.ir/browse/home-appliances/%D9%84%D9%88%D8%A7%D8%B2%D9%85-%D8%AE%D8%A7%D9%86%DA%AF%DB%8C\\\" \\\"Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894425Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
            "os" : {
              "name" : "Windows",
              "version" : "7",
              "full" : "Windows 7"
            },
            "name" : "Chrome",
            "device" : {
              "name" : "Other"
            },
            "version" : "71.0.3578.98"
          }
        }
      },
      {
        "_index" : "web-logs",
        "_id" : "GFEbPZwBB-P0iF0O5ehs",
        "_score" : 1.0,
        "_source" : {
          "source" : {
            "geo" : {
              "continent_name" : "Europe",
              "region_iso_code" : "DE-BY",
              "city_name" : "Nuremberg",
              "country_iso_code" : "DE",
              "country_name" : "Germany",
              "region_name" : "Bavaria",
              "location" : {
                "lon" : 11.0783,
                "lat" : 49.4527
              }
            },
            "as" : {
              "number" : 24940,
              "organization" : {
                "name" : "Hetzner Online GmbH"
              }
            },
            "address" : "91.98.239.11",
            "ip" : "91.98.239.11"
          },
          "url" : {
            "original" : "/image/57415/productModel/200x200"
          },
          "apache" : {
            "access" : { }
          },
          "@timestamp" : "2019-01-26T12:53:43.000Z",
          "http" : {
            "request" : {
              "referrer" : "https://www.zanbil.ir/m/filter/b219%2Cp1392?page=1",
              "method" : "GET"
            },
            "response" : {
              "status_code" : 200,
              "body" : {
                "bytes" : 5152
              }
            },
            "version" : "1.1"
          },
          "event" : {
            "ingested" : "2026-02-08T11:56:04.326181776Z",
            "original" : "91.98.239.11 - - [26/Jan/2019:16:23:43 +0330] \\\"GET /image/57415/productModel/200x200 HTTP/1.1\\\" 200 5152 \\\"https://www.zanbil.ir/m/filter/b219%2Cp1392?page=1\\\" \\\"Mozilla/5.0 (Linux; Android 8.0.0; SAMSUNG SM-A605F Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/8.2 Chrome/63.0.3239.111 Mobile Safari/537.36\\\" \\\"-\\\"",
            "kind" : "event",
            "created" : "2026-02-08T11:56:03.894431Z",
            "category" : "web",
            "outcome" : "success"
          },
          "user" : {
            "name" : "-"
          },
          "user_agent" : {
            "original" : "Mozilla/5.0 (Linux; Android 8.0.0; SAMSUNG SM-A605F Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/8.2 Chrome/63.0.3239.111 Mobile Safari/537.36",
            "os" : {
              "name" : "Android",
              "version" : "8.0.0",
              "full" : "Android 8.0.0"
            },
            "name" : "Samsung Internet",
            "device" : {
              "name" : "Samsung $2"
            },
            "version" : "8.2"
          }
        }
      }
    ]
  }
}

```

### 데이터 쿼리 실행

1. HTTP 응답 코드가 200인 모든 HTTP 이벤트 찾기

- term query를 사용

```json
GET web-logs/_search
{
    "query": {
        "term": {
            "http.response.status_code": { "value": "200" }
        }
    }
}
```

2. 요청 방식이 POST, 응답 코드가 200이 아닌 모든 HTTP 이벤트 찾기

- bool 복합 쿼리
    - must_not을 이용해 제외
    - must를 이용해 포함

```json
GET web-logs/_search
{
    "query": {
        "bool": {
            "must_not" : [
                {
                    "term": {
                        "http.response.status_code": { "value": "200" }
                    }
                }
            ],
            "must": [
                {
                    "term": {
                        "http.request.method": { "value": "POST" }
                    }
                }
            ]
        }
    }
}
```

3. 문서에서 refrigerator와 windows라는 텀을 포함하는 모든 HTTP 이벤트를 찾기

- event.original 필드에 match 쿼리를 사용
    - and 연산자를 사용하여 결과문서에 두 단어가 모두 있어야 불러옴

```json
GET web-logs/_search
{
    "query": {
        "match": {
            "event.original": {
                "query": "refrigerator windows",
                "operator": "and"
            }
        }
    }
}
```

4. 윈도우 사용자가 웹사이트에서 냉장고 관련 페이지를 보고 있는 모든 요청을 찾기

- 2개의 매치 쿼리와 bool 복합 쿼리 사용

```json
GET web-logs/_search
{
    "query": {
        "bool": {
            "must": [
                {"match": {"url.original.text": "refrigerator"}},
                {"match": {"user_agent.os.full.text": "windows"}}
            ]
        }
    }
}
```

5. 남아프리카, 아일랜드, 홍콩에서 발생한 모든 이벤트 찾기

- terms 매치 쿼리를 사용

```json
GET web-logs/_search
{
    "query": {
        "terms": {
            "source.geo.country_name": [
                "South Africa",
                "Ireland",
                "Hong Kong"
            ]
        }
    }
}
```

6. Pars Online PJS와 Respina Networks & Beyond PJSC 통신사에 속한 IP 주소에서 발생한 모든 이벤트 찾기

- 통신사 목록을 저장할 인덱스 생성
    - 쿼리의 일부로 통신사를 정의하는 것 대신에 사용할 수 있음

```json
PUT telcos-list
{
    "mappings": {
        "properties": {"name":{"type":"keyword"}}
    }
}

// 검색할 텀 목록이 포함된 문서를 색인
PUT telcos-list/_doc/1
{
    "name": ["Pars Online PJS", "Respina Networks & Beyond PJSC"]
}

// index 검색에 terms 쿼리를 사용해 히트를 찾기
GET web-logs/_search
{
    "query": {
        "terms": {
            "source.as.organization.name": {
                "index": "telcos-list",
                "id": "1",
                "path": "name"
            }
        }
    }
}
```

7. 응답 본문이 100,000 바이트를 초과하는 모든 HTTP GET 이벤트를 찾기

- bool 쿼리사용
    - GET 이벤트에 대한 텀 매치 쿼리
    - 숫자 유형의 http.response.body.bytes 필드에 대한 range 필터를 포함

```json
GET web-logs/_search
{
    "query": {
        "bool": {
            "must": [
                { "term": {"http.request.method": {"value": "GET"} }},
                { "range": {"http.response.body.bytes": {"gte": 100000}}}
            ]
        }
    }
}
```
