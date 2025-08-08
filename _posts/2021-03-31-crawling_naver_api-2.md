---
layout: post
title: "NAVER API를 사용해서 크롤링하기 - 2"
description: >-
  네이버 API를 활용한 웹 크롤링 방법과 과정에 대한 상세 가이드
author: seunghun
date: 2021-03-31 08:00:00 +0800
categories: [Data Science, Web Crawling]
tags: [crawling, data-collection, naver-api]
---

## 1. API 코드 분석

이전 포스팅에서 네이버 API를 신청하고, 애플리케이션을 등록하여 Client ID와 Secret을 발급 받았다. 이제 API Documents에서 제공하는 Python 예제 코드를 분석한다.

```python
# 네이버 검색 API 예제 - 블로그 검색
import os
import sys
import urllib.request
client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
encText = urllib.parse.quote("검색할 단어")
url = "https://openapi.naver.com/v1/search/blog?query=" + encText # JSON 결과
# url = "https://openapi.naver.com/v1/search/blog.xml?query=" + encText # XML 결과
request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id",client_id)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request)
rescode = response.getcode()
if(rescode==200):
    response_body = response.read()
    print(response_body.decode('utf-8'))
else:
    print("Error Code:" + rescode)
```

### 코드 구성 요소 분석

#### 1. 애플리케이션 인증

```python
client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
```

- 네이버 API 사용을 위한 인증 정보
- 이전 포스팅에서 발급받은 Client ID와 Secret을 입력한다.

#### 2. 검색 키워드 파싱

```python
encText = urllib.parse.quote("검색할 단어")
```

- 검색할 단어를 URL 인코딩한다.
- 한글과 특수문자는 그대로 전달할 수 없으므로 인코딩이 필요하다.
- 예시: "코로나" → '%EC%BD%94%EB%A1%9C%EB%82%98'

#### 3. 요청 URL 구성

```python
url = "https://openapi.naver.com/v1/search/blog?query=" + encText #json 결과

url = "https://openapi.naver.com/v1/search/blog.xml?query=" + encText # xml 결과
```

- 검색 결과는 JSON 또는 XML 형식으로 제공된다.
- 기본값은 JSON 형식이며, XML을 원할 경우 `.xml` 확장자를 사용한다.

![API 정보](/assets/img/posts/crawling_naver_api/api_information.png)

#### 4. 요청 및 응답 처리

```python
request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id", client_id)
request.add_header("X-Naver-Client-Secret", client_secret)

response = urllib.request.urlopen(request)
rescode = response.getcode()

if(rescode == 200):
    response_body = response.read()
    print(response_body.decode('utf-8'))
else:
    print("Error Code:" + rescode)
```

- 서버에 요청을 보내고 응답을 받는다.
- HTTP 상태 코드 200은 정상 응답을 의미한다.
- 응답 데이터는 UTF-8로 디코딩하여 출력한다.

### 검색 결과 예시

"코로나" 키워드로 검색한 결과:
![코로나 검색 결과](/assets/img/posts/crawling_naver_api/result_of_corona.png)

검색 결과 필드 설명:
![결과 정보](/assets/img/posts/crawling_naver_api/result_information.png)

네이버 블로그 직접 검색 결과와 비교:
![블로그 검색 결과](/assets/img/posts/crawling_naver_api/result_of_corona_blog.png)

### 에러 코드
요청이 실패할 경우 발생하는 에러 코드들:
![에러 코드](/assets/img/posts/crawling_naver_api/error_code.png)

## 2. 요청 변수 설정

검색 결과에서 `start`와 `display` 파라미터를 확인할 수 있다:
- `start`: 검색 시작 위치
- `display`: 출력할 결과 개수

### 사용 가능한 요청 변수
![요청 변수](/assets/img/posts/crawling_naver_api/request_variable.png)

### 요청 변수 사용 예시

```bash
curl "https://openapi.naver.com/v1/search/blog.xml?query=%EB%A6%AC%EB%B7%B0&display=10&start=1&sort=sim" \
    -H "X-Naver-Client-Id: {client_id}" \
    -H "X-Naver-Client-Secret: {client_secret}" -v
```

- 검색어: query=`%EB%A6%AC%EB%B7%B0`, 리뷰
- 출력 개수: display=10, 10개
- 시작 위치: start=1, 1페이지
- 정렬: sort=sim, 유사도순
