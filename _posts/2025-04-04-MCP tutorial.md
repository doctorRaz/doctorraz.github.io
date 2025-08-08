---
title: Claude App에서 MCP(Model Context Protocol) 설정하기
description: >-
  Claude App에서 MCP(Model Context Protocol)를 설정하는 기본적인 방법을 알아본다.
author: seunghun
date: 2025-04-03 13:00:00
categories: [AI, Development]
tags: [MCP, Claude, AI, Protocol, Tutorial]
pin: false
render_with_liquid: false
media_subpath: 
---

## MCP란?

MCP는 애플리케이션이 LLM에 컨텍스트를 제공하는 방식을 표준화하는 개방형 프로토콜이다. MCP는 AI 애플리케이션을 위한 USB-C 포트와 같다. USB-C가 다양한 주변 장치와 액세서리에 기기를 연결하는 표준화된 방법을 제공하는 것처럼, MCP는 AI 모델을 다양한 데이터 소스와 도구에 연결하는 표준화된 방법을 제공한다.

![MCP architecture](/assets/img/posts/MCP/MCP_architecture.png)

## MCP 설정 방법

### 1. Claude APP 설치
- Claude App 다운로드: <https://claude.ai/download>

### 2. MCP 서버 선택
다음 사이트에서 사용할 MCP 서버를 선택할 수 있다:
- <https://mcpservers.org/>
- <https://www.pulsemcp.com/servers>
- <https://smithery.ai/>

이 예제에서는 Filesystem 서버를 사용하여 컴퓨터의 파일을 읽고 쓰는 방법을 알아보자.

1. Pulse 홈페이지에서 Filesystem 서버를 선택한다.
![pulse_filesystem](/assets/img/posts/MCP/pulse_filesystem.png)

2. npm 패키지 설정 방법을 선택한다.
![pulse_filesystem2](/assets/img/posts/MCP/pulse_filesystem2.png)

3. NPX 코드를 복사한다. 아래 코드는 지정된 경로에 대한 파일 읽기/쓰기 권한을 부여한다. 따라서, 나의 환경에 맞게 알맞은 폴더 경로를 지정해야 된다.
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/username/Desktop",
        "/path/to/other/allowed/dir"
      ]
    }
  }
}
```

예시: 바탕화면과 다운로드 폴더에 대한 권한 설정
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/seunghun/Desktop",
        "/Users/seunghun/Downloads"
      ]
    }
  }
}
```

### 3. Claude APP에 서버 설치

1. Claude APP 실행
2. [File] → [Setting] → [Developer] → [Edit Config] 클릭
![Claude_settings](/assets/img/posts/MCP/claude_settings.png)

3. Claude APP 설치 폴더에서 **claude_desktop_config.json** 파일을 열고 복사한 NPX 코드를 붙여넣는다.
![Claude_folder](/assets/img/posts/MCP/claude_folder.png)
![claude_desktop_config](/assets/img/posts/MCP/claude_desktop_config.png)

4. Claude APP을 재시작한다.

### 4. MCP 도구 확인

재시작 후 망치 아이콘이 표시되며, 현재 11개의 MCP 도구를 사용할 수 있다.
![claude](/assets/img/posts/MCP/claude.png)

망치 아이콘을 클릭하면 사용 가능한 MCP 도구 목록을 확인할 수 있다:
- create_directory: 디렉토리 생성
- directory_tree: 디렉토리 구조 확인
- edit_file: 파일 수정
등의 파일 및 폴더 관련 작업을 수행할 수 있다.
![MCPtools](/assets/img/posts/MCP/MCPtools.png)

### 5. 파일 쓰기 예제

MCP 도구를 사용하여 실제 파일을 생성하고 내용을 작성하는 예제를 살펴보자.

1. **파일 생성 요청**
   - 다운로드 폴더에 'MCP.txt' 파일을 생성하고 MCP에 대한 설명을 작성하도록 요청한다.
   ![prompt](/assets/img/posts/MCP/prompt.png)

2. **도구 권한 요청**
   - Claude가 필요한 MCP 도구를 자동으로 선택하고 사용 권한을 요청한다.
   ![Request_use_tool](/assets/img/posts/MCP/Request_use_tool.png)

3. **결과 확인**
   - 다운로드 폴더에 'MCP.txt' 파일이 생성됐다.
   - 파일 내용을 확인하면 MCP에 대한 상세한 설명이 정상적으로 작성된 것을 확인할 수 있다.
   ![result1](/assets/img/posts/MCP/result1.png)
   ![result2](/assets/img/posts/MCP/result2.png)
   ![result3](/assets/img/posts/MCP/result3.png)


## MCP 서버 보안 주의사항

MCP 서버를 사용할 때는 보안에 특별히 주의해야 한다:

1. **보안 위험성**
   - 무분별하거나 인증되지 않은 MCP 서버를 사용할 경우 보안 위협이 발생할 수 있다.
   - MCP 서버 코드에 악성 코드가 숨겨져 있을 경우 시스템이 쉽게 해킹될 수 있다.

2. **안전한 MCP 서버 선택 방법**
   - MCP 서버를 공식적으로 제공하는 제공자의 서버를 사용한다.
   - 믿을 수 있는 곳에서 배포하는 MCP 서버를 선택한다.
   - Pulse MCP와 같은 플랫폼에서는 "Official Providers" 인증 마크가 있는 서버를 우선적으로 고려한다.
