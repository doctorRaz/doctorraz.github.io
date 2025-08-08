---
title: "정적 웹 크롤링: 웹 데이터 수집의 기초"
description: >-
  정적 웹 크롤링의 개념과 Python을 활용한 기본적인 웹 데이터 수집 방법을 다룬다.
  BeautifulSoup과 requests 라이브러리를 사용한 실전 예제와 함께 정적 웹 크롤링의 핵심 개념을 설명한다.
author: seunghun
date: 2025-04-06 12:00:00 +0800
categories: [Data Science, Web Crawling]
tags: [crawling, data-collection, static]
---

## 웹 크롤링이란?

웹 크롤링(Web Crawling)은 자동화된 방법으로 웹 페이지에서 정보를 수집하는 과정이다. 웹 크롤러(Web Crawler)라고 불리는 프로그램이 웹 페이지를 방문하여 데이터를 추출하고, 해당 페이지의 링크를 따라 다른 페이지로 이동하며 정보를 수집한다.

웹 크롤링은 크게 두 가지 유형으로 나눌 수 있다:

1. **정적 웹 크롤링(Static Web Crawling)**: HTML 소스 코드에서 직접 데이터를 추출하는 방식이다. 페이지가 로드될 때 서버에서 전송된 HTML 내용만을 분석한다.

2. **동적 웹 크롤링(Dynamic Web Crawling)**: JavaScript로 동적으로 생성되는 콘텐츠를 포함하여 데이터를 추출하는 방식이다. 브라우저 렌더링 과정을 시뮬레이션하여 동적으로 로드되는 콘텐츠까지 수집할 수 있다.

## 정적 웹 크롤링 vs 동적 웹 크롤링

정적 웹 크롤링과 동적 웹 크롤링은 각각 다른 상황에서 유용하며, 서로 다른 장단점을 가지고 있다. 아래 표는 두 방식의 주요 차이점을 비교한 것이다:

| 특성 | 정적 웹 크롤링 | 동적 웹 크롤링 |
|------|--------------|--------------|
| **대상 콘텐츠** | 서버에서 직접 전송된 HTML 소스 코드 | JavaScript로 동적 생성되는 콘텐츠 포함 |
| **필요 라이브러리** | requests, BeautifulSoup 등 | Selenium, Playwright, Puppeteer 등 |
| **처리 속도** | 빠름 | 상대적으로 느림 (브라우저 렌더링 필요) |
| **리소스 사용** | 적음 | 많음 (메모리, CPU 사용량 높음) |
| **구현 복잡도** | 간단함(단순 HTTP 요청 및 파싱) | 복잡함 (브라우저 자동화 설정 및 제어 필요) |
| **적합한 사이트** | 정적 HTML 기반 사이트 | SPA(Single Page Application), AJAX 기반 현대적 웹사이트 |
| **JavaScript 처리** | 불가능 | 가능 |
| **사용자 상호작용** | 제한적(요청 위주) | 클릭, 스크롤, 입력 등 다양한 상호작용 가능 |
| **헤드리스 모드** | 필요 없음 | 지원 (UI 없이 백그라운드 실행) |
| **차단 가능성** | 낮음 (단순 HTTP 요청) | 상대적으로 높음 (봇 탐지 시스템에 감지될 가능성) |

이 글에서는 정적 웹 크롤링에 초점을 맞추어 설명하겠다. 동적 웹 크롤링에 대해서는 별도의 글에서 다룰 예정이다.


## 정적 웹 크롤링 절차

정적 웹 크롤링은 다음과 같은 기본 절차로 진행된다:

1. **필요한 라이브러리 설치**

정적 웹 크롤링을 위해서는 다음과 같은 Python 라이브러리들이 필요하다:

```bash
pip install requests  # HTTP 요청을 보내기 위한 라이브러리
pip install beautifulsoup4  # HTML 파싱을 위한 라이브러리
pip install pandas  # 데이터 처리를 위한 라이브러리
```

2. **HTTP 요청 보내기**

웹 페이지의 HTML 내용을 가져오기 위해 HTTP GET 요청을 보낸다.

```python
# 필요한 라이브러리 임포트
import requests
from bs4 import BeautifulSoup
import pandas as pd
import time

# arXiv 검색 페이지 URL 설정
query = "LLM"
url = f"https://arxiv.org/search/?query={query}&searchtype=all&source=header&start=0"

# User-Agent 설정 (웹사이트 차단 방지)
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36'
}

# 페이지 요청
response = requests.get(url, headers=headers)
print(f"Status Code: {response.status_code}")  # 200이면 성공
```

> User-Agent를 설정하면 웹사이트가 봇이 아닌 일반 브라우저로 인식하게 할 수 있다. 랜덤 User-Agent를 사용하려면 다음과 같이 구현할 수 있다:
{: .prompt-tip }

```python
import random

# 다양한 User-Agent 목록
user_agents = [
    'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36',
    'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Safari/605.1.15',
    'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.107 Safari/537.36',
    'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:90.0) Gecko/20100101 Firefox/90.0'
]

# 랜덤 User-Agent 선택
headers = {'User-Agent': random.choice(user_agents)}
```

작성 중~~~~


<!-- 
1. **HTML 파싱하기**

BeautifulSoup을 사용하여 HTML 내용을 파싱한다.

```python
# HTML 파싱
soup = BeautifulSoup(response.text, 'html.parser')

# 검색 결과 목록 찾기
results = soup.find_all('li', class_='arxiv-result')
print(f"Found {len(results)} papers")

# 첫 번째 논문 정보 확인
first_paper = results[0]
print("\n첫 번째 논문 HTML 구조:")
print(first_paper.prettify()[:500])  # HTML 구조 확인
```

4. **데이터 추출 및 정제**

각 논문의 정보를 추출하고 정리한다.

```python
# 데이터를 저장할 리스트 생성
papers = []

# 각 논문 정보 추출
for paper in results:
    # 제목 추출
    title = paper.find('p', class_='title').text.strip()
    
    # 저자 추출
    authors = paper.find('p', class_='authors').text.strip()
    
    # Abstract 추출
    abstract = paper.find('span', class_='abstract-full').text.strip()
    
    # 제출일 추출
    submitted = paper.find('p', class_='submitted-date').text.strip()
    
    # 논문 정보를 딕셔너리로 저장
    paper_info = {
        'title': title,
        'authors': authors,
        'abstract': abstract,
        'submitted': submitted
    }
    papers.append(paper_info)

# 첫 번째 논문 정보 출력해서 확인
print("\n첫 번째 논문 정보:")
for key, value in papers[0].items():
    print(f"\n{key}:")
    print(value[:200] + "..." if len(value) > 200 else value)
```

5. **데이터 저장 및 활용**

수집한 데이터를 pandas DataFrame으로 변환하고 CSV 파일로 저장한다.

```python
# DataFrame 생성
df = pd.DataFrame(papers)

# 데이터 정제
df['title'] = df['title'].str.replace('\n', ' ').str.strip()
df['authors'] = df['authors'].str.replace('\n', ', ').str.strip()
df['abstract'] = df['abstract'].str.replace('\n', ' ').str.strip()

# 날짜 형식 변환
df['submitted'] = pd.to_datetime(df['submitted'].str.extract(r'(\d{1,2} [A-Za-z]+ \d{4})')[0])

# 결과 확인
print("\nDataFrame 정보:")
print(df.info())

print("\n첫 5개 논문 제목:")
print(df['title'].head())

# CSV 파일로 저장
filename = 'arxiv_papers.csv'
df.to_csv(filename, index=False, encoding='utf-8')
print(f"\n데이터가 {filename}에 저장되었습니다.")
```

6. **에러 처리 및 예외 상황 대응**

실제 크롤링 시에는 다음과 같은 예외 처리가 필요하다:

```python
# 예외 처리 예시
try:
    # 페이지 요청
    response = requests.get(url, headers=headers, timeout=10)
    response.raise_for_status()  # HTTP 에러 체크
    
    # 페이지 파싱
    soup = BeautifulSoup(response.text, 'html.parser')
    results = soup.find_all('li', class_='arxiv-result')
    
    if not results:  # 결과가 없는 경우
        print("검색 결과가 없습니다.")
        
except requests.exceptions.RequestException as e:
    print(f"요청 중 오류 발생: {e}")
except Exception as e:
    print(f"처리 중 오류 발생: {e}")
finally:
    # 요청 간격 준수
    time.sleep(1)
``` -->