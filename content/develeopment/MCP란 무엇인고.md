---
tags:
  - MCP
  - ai
  - model
  - context
  - protocol
date: 2025-04-03
---
## MCP란 무엇인가?

MCP(Model Context Protocol - 모델 컨텍스트 프로토콜)는 AI 모델이 외부 데이터 소스 및 도구와 원활하게 연결될 수 있도록 설계된 개방형 표준 프로토콜이다. 2024년 11월에 Anthropic에 의해 오픈 소스로 공개된 이 기술은 AI 시스템이 실시간으로 데이터를 접근하고, 다양한 작업을 수행할 수 있도록 지원한다. MCP는 AI 모델이 정보의 고립에서 벗어나, 필요한 데이터를 쉽게 가져올 수 있도록 도와준다.

### MCP의 주요 구성 요소

MCP는 다음 세 가지 주요 구성 요소로 이루어져 있다.

- **호스트(Host)**: AI 모델을 운용하는 애플리케이션으로, 사용자로부터 질문이나 명령을 받아 모델에게 전달한다. 예를 들어, Claude Desktop이나 IDE의 AI 어시스턴트가 이에 해당한다.
- **클라이언트(Client)**: 호스트 애플리케이션 내에서 서버와 1:1 연결을 유지하는 시스템으로, 클라이언트는 요청을 보내고 응답을 받아 모델에 전달하는 역할을 한다.
- **서버(Server)**: 외부 데이터나 기능을 제공하는 시스템으로, 클라이언트의 요청에 따라 필요한 정보를 제공한다.

### MCP에서의 도구(Tools)

MCP에서 "도구"는 AI 모델이 외부 시스템과 상호작용할 수 있도록 해주는 기능적 모듈을 의미한다. 도구는 서버에서 클라이언트로 노출되며, AI 모델이 이를 호출하여 다양한 작업을 수행할 수 있게 한다.

- **실행 가능성**: 도구는 AI 모델이 외부 시스템과 상호작용하고, 계산을 수행하며, 실제 세계에서 행동을 취할 수 있도록 해준다. 예를 들어, 날씨 정보를 가져오거나 데이터베이스에서 쿼리를 실행하는 등의 작업을 수행할 수 있다.
- **동적 발견**: 클라이언트는 MCP 서버를 통해 사용 가능한 도구 목록을 조회할 수 있으며, 이를 통해 필요한 도구를 쉽게 찾고 사용할 수 있다.
- **유연성**: 도구는 간단한 계산부터 복잡한 API 상호작용까지 다양한 기능을 포함할 수 있다. 이는 AI 모델이 다양한 상황에 맞춰 적절한 도구를 선택하여 사용할 수 있게 한다.

#### 도구의 예시

- **검색 도구**: 웹 검색을 통해 최신 정보를 가져오는 기능을 제공하는 도구
- **데이터 과학 도구**: 데이터 탐색, 분석 및 시각화를 지원하는 도구
- **클라우드 플랫폼 도구**: 클라우드 기반 데이터 및 서비스에 대한 접근을 제공
- **버전 관리 도구**: 코드 및 문서의 버전 관리를 지원하는 도구
- **개발자 도구**: AI 기반 코드 편집 및 디버깅 기능을 제공하는 도구

### 마무리

MCP는 AI 모델이 외부 데이터와 상호작용하고, 다양한 작업을 수행할 수 있도록 돕는 중요한 요소다. 이러한 도구들은 AI의 활용 범위를 넓히고, 실시간 데이터 접근을 가능하게 하여 AI 시스템의 성능을 크게 향상시킬 수 있다. MCP는 AI 기술의 다음 단계를 여는 중요한 전환점이 될 가능성이 높으며, 다양한 서비스와 도구들이 MCP를 채택함에 따라 더욱 발전할 것 같다.

---

## 참조

- [https://www.anthropic.com/news/model-context-protocol](https://www.anthropic.com/news/model-context-protocol)
- [https://microsoft.github.io/genaiscript/reference/scripts/mcp-tools/](https://microsoft.github.io/genaiscript/reference/scripts/mcp-tools/)
- [https://medium.com/data-and-beyond/the-model-context-protocol-mcp-the-ultimate-guide-c40539e2a8e7](https://medium.com/data-and-beyond/the-model-context-protocol-mcp-the-ultimate-guide-c40539e2a8e7)