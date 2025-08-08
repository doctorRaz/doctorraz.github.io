---
layout: post
title: "NAVER API를 사용해서 크롤링하기 - 1"
description: >-
  네이버 API를 활용한 웹 크롤링 방법과 과정에 대한 상세 가이드
author: seunghun
date: 2021-03-29 08:00:00 +0800
categories: [Data Science, Web Crawling]
tags: [crawling, data-collection, naver-api]
---

## 1. 네이버 개발자 API 가입 & 이용 신청

네이버 API를 사용하기 위해서는 우선 네이버 개발자 센터에 가입하고 오픈 API 이용 신청을 해야 한다.  
아래 링크에서 신청을 진행할 수 있다.

네이버 개발자 센터 : <https://developers.naver.com/main/>
![developers_naver_main](/assets/img/posts/crawling_naver_api/developers_naver_main.png)

### 애플리케이션 등록 과정

1. 개발자 센터 메인 페이지에서 [Application] - [애플리케이션 등록]을 클릭한다.
2. 약관 동의와 계정 정보를 등록한다.
3. 아래와 같이 애플리케이션 등록 페이지가 표시된다:
![Application_registration](/assets/img/posts/crawling_naver_api/Application_registration.png)

### 애플리케이션 설정

- **애플리케이션 이름**: 원하는 이름을 입력한다.
- **사용 API**: 검색 API를 선택한다.
- **비 로그인 오픈 API 서비스 환경**: 
  - Android, IOS, WEB 중 선택 가능
  - 로컬 컴퓨터 WEB 환경에서 사용하므로 WEB 선택
  - URL은 `<http://localhost>` 입력

### 등록 완료 후 정보 확인

![Application_information](/assets/img/posts/crawling_naver_api/Application_information.png)

등록이 완료되면 위와 같이 애플리케이션 정보를 확인할 수 있다:

- **Client ID와 Client Secret**: API 사용 시 필요한 인증 정보이므로 반드시 기록해둔다.
- **API 사용량 제한**: 
  - 일반 사용자는 하루 25,000회로 제한
  - 더 많은 사용량이 필요한 경우 API 제휴 신청 필요

## 2. 검색 API Documents

네이버 개발자 메인 페이지에서 다음 경로로 API 문서를 확인할 수 있다:
[Documents] → [서비스 API] → [검색]

![search_api_documents](/assets/img/posts/crawling_naver_api/search_api_documents.png)

### 블로그 검색 API Python 코드 예제

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

다음 포스팅에서는 위의 Python 코드를 사용하여 실제 데이터 크롤링을 진행해본다.