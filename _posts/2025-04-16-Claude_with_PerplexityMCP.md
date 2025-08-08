---
title: Claude 앱에 Perplexity MCP 서버 구축하기
description: >-
  Claude 애플리케이션에 Perplexity MCP 서버를 연동하는 방법
author: seunghun
date: 2025-04-16 22:00:00 +0800
categories: [AI, Development]
tags: [Claude, Perplexity, MCP, AI, Tutorial]
---


## 소개

이 포스트에서는 Claude 앱에 Perplexity MCP 서버를 연동하는 방법을 알아본다. MCP(Model Context Protocol)의 기본 개념과 설정 방법에 대해서는 [Claude App에서 MCP(Model Context Protocol) 설정하기](/posts/MCP-tutorial/) 포스트를 참고한다.

Perplexity MCP 서버를 통해 Claude는 실시간 웹 검색 기능을 활용할 수 있게 되어, 최신 정보에 기반한 응답을 제공할 수 있다. 이 글에서는 Perplexity MCP 서버 설정에 초점을 맞추어 설명한다.

공식적인 가이드는 아래 링크에서 확인 할 수 있다. 
- [Integrating MCP with Perplexity's Sonar API](https://docs.perplexity.ai/guides/mcp-server)

## Perplexity 사용의 장점

Perplexity MCP 서버를 Claude와 통합하면 다음과 같은 주요 장점들이 있습니다:

1. **실시간 정보 접근과 신뢰성 향상**
   - 정보에 기반한 응답 제공
   - 시시각각 변하는 데이터에 대한 정확한 정보 전달
   - 실시간 이벤트와 트렌드에 대한 즉각적인 대응 가능
   - 다양한 웹 소스를 통한 정보 검증
   - 최신 연구 및 공식 문서 참조 가능
   - 출처를 명확히 제시할 수 있는 기능

이러한 장점들을 통해 Claude는 단순한 AI 챗봇을 넘어, 실시간 정보를 활용한 지능형 비서로서의 역할을 수행할 수 있게 됩니다.


## Perplexity MCP 서버 설정하기

### 1. Perplexity MCP 서버 찾기

Perplexity MCP 서버는 대표적인 MCP 서버 제공 사이트인 Pulse MCP(https://www.pulsemcp.com/)에서 찾을 수 있다. Perplexity 서버는 다음 링크에서 확인할 수 있으며 아래 그림과 같이 나온다:
- [Perplexity MCP 서버](https://www.pulsemcp.com/servers?classification%5B%5D=official-providers&q=perplexity)
![Perplexity MCP 서버](/assets/img/posts/Claude_Perplexity/PerplexityMCP.png)

### 2. Perplexity MCP 서버 설정 코드 가져오기

위 링크에서 공식 Perplexity MCP 서버를 제공하는 GitHub 저장소([https://github.com/ppl-ai/modelcontextprotocol](https://github.com/ppl-ai/modelcontextprotocol))로 이동하면 필요한 npx 코드를 확인할 수 있다.

Perplexity MCP 서버 설정을 위한 JSON 코드는 다음과 같다:

```json
{
  "mcpServers": {
    "perplexity-ask": {
      "command": "npx",
      "args": [
        "-y",
        "server-perplexity-ask"
      ],
      "env": {
        "PERPLEXITY_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

위 코드에서 `YOUR_API_KEY_HERE`에는 Perplexity 에서 발급 받은 API 키를 입력하면 된다. 그리고 Claude 앱의 `claude_desktop_config.json` 설정 파일에 위의 Perplexity MCP Server NPX 코드를 추가하고 Claude 앱을 재시작하면 설정이 완료 된다.


## Perplexity MCP 서버 활용 예시

Claude 앱에서 Perplexity MCP 서버를 활용하여 인터넷 검색을 수행하는 과정을 살펴본다. 아래 예시에서는 Perplexity에 대한 최신 업데이트 정보를 검색한다.

먼저 Claude에 인터넷 검색을 통한 정보 요청을 입력한다.
![Example 1_1](/assets/img/posts/Claude_Perplexity/example1_1.png)

Claude는 인터넷 검색 기능을 위해 Perplexity MCP 서버 사용 권한을 요청한다.
![Example 1_2](/assets/img/posts/Claude_Perplexity/example1_2.png)

권한 승인 후 Claude는 Perplexity 검색 결과를 정리하여 응답을 제공한다.
![Example 1_3](/assets/img/posts/Claude_Perplexity/example1_3.png)