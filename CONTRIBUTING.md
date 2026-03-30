# Contributing to nanobot

Thank you for being here.

nanobot is built with a simple belief: good tools should feel calm, clear, and humane.
We care deeply about useful features, but we also believe in achieving more with less:
solutions should be powerful without becoming heavy, and ambitious without becoming
needlessly complicated.

This guide is not only about how to open a PR. It is also about how we hope to build
software together: with care, clarity, and respect for the next person reading the code.

## Maintainers

| Maintainer | Focus |
|------------|-------|
| [@re-bin](https://github.com/re-bin) | Project lead, `main` branch |
| [@chengyongru](https://github.com/chengyongru) | `nightly` branch, experimental features |

## Branching Strategy

We use a two-branch model to balance stability and exploration:

| Branch | Purpose | Stability |
|--------|---------|-----------|
| `main` | Stable releases | Production-ready |
| `nightly` | Experimental features | May have bugs or breaking changes |

### Which Branch Should I Target?

**Target `nightly` if your PR includes:**

- New features or functionality
- Refactoring that may affect existing behavior
- Changes to APIs or configuration

**Target `main` if your PR includes:**

- Bug fixes with no behavior changes
- Documentation improvements
- Minor tweaks that don't affect functionality

**When in doubt, target `nightly`.** It is easier to move a stable idea from `nightly`
to `main` than to undo a risky change after it lands in the stable branch.

### How Does Nightly Get Merged to Main?

We don't merge the entire `nightly` branch. Instead, stable features are **cherry-picked** from `nightly` into individual PRs targeting `main`:

```
nightly  ──┬── feature A (stable) ──► PR ──► main
           ├── feature B (testing)
           └── feature C (stable) ──► PR ──► main
```

This happens approximately **once a week**, but the timing depends on when features become stable enough.

### Quick Summary

| Your Change | Target Branch |
|-------------|---------------|
| New feature | `nightly` |
| Bug fix | `main` |
| Documentation | `main` |
| Refactoring | `nightly` |
| Unsure | `nightly` |

## Development Setup

Keep setup boring and reliable. The goal is to get you into the code quickly:

```bash
# Clone the repository
git clone https://github.com/HKUDS/nanobot.git
cd nanobot

# Install with dev dependencies
pip install -e ".[dev]"

# Run tests
pytest

# Lint code
ruff check nanobot/

# Format code
ruff format nanobot/
```

## Code Style

We care about more than passing lint. We want nanobot to stay small, calm, and readable.

When contributing, please aim for code that feels:

- Simple: prefer the smallest change that solves the real problem
- Clear: optimize for the next reader, not for cleverness
- Decoupled: keep boundaries clean and avoid unnecessary new abstractions
- Honest: do not hide complexity, but do not create extra complexity either
- Durable: choose solutions that are easy to maintain, test, and extend

In practice:

- Line length: 100 characters (`ruff`)
- Target: Python 3.11+
- Linting: `ruff` with rules E, F, I, N, W (E501 ignored)
- Async: uses `asyncio` throughout; pytest with `asyncio_mode = "auto"`
- Prefer readable code over magical code
- Prefer focused patches over broad rewrites
- If a new abstraction is introduced, it should clearly reduce complexity rather than move it around

## Questions?

If you have questions, ideas, or half-formed insights, you are warmly welcome here.

Please feel free to open an [issue](https://github.com/HKUDS/nanobot/issues), join the community, or simply reach out:

- [Discord](https://discord.gg/MnCvHqpUGB)
- [Feishu/WeChat](./COMMUNICATION.md)
- Email: Xubin Ren (@Re-bin) — <xubinrencs@gmail.com>

Thank you for spending your time and care on nanobot. We would love for more people to participate in this community, and we genuinely welcome contributions of all sizes.


nanobot (0.1.4.post6)
├── 1. Core Framework & Utilities (코어 프레임워크 및 유틸리티)
│   ├── pydantic (>=2.12.0)
│   │   ├── annotated-types
│   │   ├── pydantic-core
│   │   └── typing-extensions
│   ├── pydantic-settings (>=2.12.0)
│   │   ├── pydantic
│   │   └── python-dotenv
│   ├── typer (>=0.20.0)
│   │   ├── click
│   │   └── typing_extensions
│   ├── loguru (>=0.7.3)           # 로깅 유틸리티
│   ├── croniter (>=6.0.0)         # 크론 탭 형식 스케줄러
│   │   ├── python-dateutil
│   │   └── pytz
│   └── msgpack (>=1.1.0)          # 데이터 직렬화
│
├── 2. AI & LLM Providers (AI 및 언어 모델)
│   ├── openai (>=2.8.0)
│   │   ├── anyio
│   │   ├── distro
│   │   ├── httpx
│   │   ├── pydantic
│   │   ├── sniffio
│   │   ├── tqdm
│   │   └── typing-extensions
│   ├── anthropic (>=0.45.0)
│   │   ├── anyio
│   │   ├── httpx
│   │   ├── pydantic
│   │   └── tokenizers
│   └── tiktoken (>=0.12.0)        # 토큰화 라이브러리
│       ├── regex
│       └── requests
│
├── 3. Networking & HTTP Clients (네트워크 및 통신)
│   ├── httpx (>=0.28.0)
│   │   ├── anyio
│   │   ├── certifi
│   │   ├── httpcore
│   │   ├── idna
│   │   └── sniffio
│   ├── websockets (>=16.0)
│   ├── websocket-client (>=1.9.0)
│   ├── python-socks[asyncio] (>=2.8.0)
│   │   └── async-timeout
│   └── socksio (>=1.0.0)
│
├── 4. Messaging & Chat Channels (메신저 채널 연동)
│   ├── python-telegram-bot[socks] (>=22.6)
│   │   ├── httpx
│   │   └── cryptography
│   ├── slack-sdk (>=3.39.0)
│   ├── slackify-markdown (>=0.2.0)
│   ├── qq-botpy (>=1.2.0)
│   │   ├── aiohttp
│   │   └── pyyaml
│   ├── lark-oapi (>=1.5.0)        # Feishu/Lark 연동
│   │   ├── requests
│   │   └── requests-toolbelt
│   ├── dingtalk-stream (>=0.24.0) # DingTalk 연동
│   └── python-socketio (>=5.16.0) # MoChat 등 소켓 연동
│       ├── bidict
│       └── python-engineio
│           └── simple-websocket
│
├── 5. Tools & Protocols (웹 검색, 포맷팅, MCP)
│   ├── ddgs (>=9.5.5)             # DuckDuckGo 웹 검색
│   │   ├── curl-cffi
│   │   └── lxml
│   ├── mcp (>=1.26.0)             # Model Context Protocol
│   │   ├── anyio
│   │   └── pydantic
│   ├── readability-lxml (>=0.8.4) # 웹 페이지 본문 추출
│   │   ├── chardet (>=3.0.2)
│   │   ├── cssselect
│   │   └── lxml
│   ├── json-repair (>=0.57.0)     # 불완전한 JSON 파싱 보정
│   └── oauth-cli-kit (>=0.1.3)
│
├── 6. CLI Interface & Terminal (터미널 UI)
│   ├── rich (>=14.0.0)
│   │   ├── markdown-it-py
│   │   └── pygments
│   ├── prompt-toolkit (>=3.0.50)
│   │   └── wcwidth
│   └── questionary (>=2.0.0)
│       └── prompt-toolkit
│
└── 7. Optional Dependencies (선택적 추가 패키지)
    ├── wecom (위챗 워크)
    │   └── wecom-aibot-sdk-python
    ├── weixin (위챗)
    │   ├── qrcode[pil]
    │   └── pycryptodome
    ├── matrix (Matrix 메신저)
    │   ├── matrix-nio[e2e]
    │   ├── mistune
    │   └── nh3
    ├── langsmith (디버깅)
    │   └── langsmith
    └── dev (개발/테스트 도구)
        ├── pytest
        ├── pytest-asyncio
        ├── pytest-cov
        └── ruff (Linter)



        ---


        - **nanobot** (0.1.4.post6) [48 KB]
  - **1. Core Framework & Utilities**
    - pydantic (>=2.12.0) [407 KB]
      - annotated-types [16 KB]
      - pydantic-core [2150 KB]
      - typing-extensions [38 KB]
    - pydantic-settings (>=2.12.0) [44 KB]
      - python-dotenv [24 KB]
    - typer (>=0.20.0) [45 KB]
      - click [98 KB]
    - loguru (>=0.7.3) [63 KB]
    - croniter (>=6.0.0) [54 KB]
      - python-dateutil [228 KB]
      - pytz [505 KB]
    - msgpack (>=1.1.0) [334 KB]

  - **2. AI & LLM Providers**
    - openai (>=2.8.0) [423 KB]
      - anyio [93 KB]
      - distro [16 KB]
      - sniffio [6 KB]
      - tqdm [79 KB]
    - anthropic (>=0.45.0) [164 KB]
      - tokenizers [3150 KB]
    - tiktoken (>=0.12.0) [1120 KB]
      - regex [384 KB]

  - **3. Networking & HTTP Clients**
    - httpx (>=0.28.0) [74 KB]
      - certifi [167 KB]
      - httpcore [80 KB]
      - idna [60 KB]
    - websockets (>=16.0) [154 KB]
    - websocket-client (>=1.9.0) [59 KB]
    - python-socks[asyncio] (>=2.8.0) [42 KB]
      - async-timeout [14 KB]
    - socksio (>=1.0.0) [24 KB]

  - **4. Messaging & Chat Channels**
    - python-telegram-bot[socks] (>=22.6) [621 KB]
      - cryptography [4250 KB]
    - slack-sdk (>=3.39.0) [325 KB]
    - slackify-markdown (>=0.2.0) [12 KB]
    - qq-botpy (>=1.2.0) [78 KB]
      - aiohttp [1150 KB]
      - pyyaml [185 KB]
    - lark-oapi (>=1.5.0) [380 KB]
      - requests-toolbelt [55 KB]
      - requests [65 KB]
    - dingtalk-stream (>=0.24.0) [22 KB]
    - python-socketio (>=5.16.0) [80 KB]
      - bidict [35 KB]
      - python-engineio [60 KB]
        - simple-websocket [14 KB]

  - **5. Tools & Protocols**
    - ddgs (>=9.5.5) [45 KB]
      - curl-cffi [12450 KB]
      - lxml [5320 KB]
    - mcp (>=1.26.0) [45 KB]
    - readability-lxml (>=0.8.4) [42 KB]
      - chardet (>=3.0.2) [202 KB]
      - cssselect [19 KB]
    - json-repair (>=0.57.0) [36 KB]
    - oauth-cli-kit (>=0.1.3) [14 KB]

  - **6. CLI Interface & Terminal**
    - rich (>=14.0.0) [245 KB]
      - markdown-it-py [86 KB]
      - pygments [1250 KB]
    - prompt-toolkit (>=3.0.50) [392 KB]
      - wcwidth [35 KB]
    - questionary (>=2.0.0) [42 KB]

  - **7. Optional Dependencies (선택 설치)**
    - wecom [200 KB]
    - weixin [15 KB]
      - qrcode[pil] [40 KB]
      - pycryptodome [14850 KB]
    - matrix [30 KB]
      - matrix-nio[e2e] [215 KB]
      - mistune [310 KB]
      - nh3 [2010 KB]
    - langsmith [180 KB]
    - dev [15 KB]
      - pytest [320 KB]
      - pytest-asyncio [45 KB]
      - pytest-cov [60 KB]
      - ruff [30210 KB]
     
| package-name | Size(KB) | etc |
| :--- | :--- | :--- |
| **nanobot** (0.1.4.post6) | 48 | 초경량 AI 에이전트 프레임워크 핵심 코드 |
| **[1. Core Framework & Utilities]** | - | **코어 프레임워크 및 유틸리티** |
| pydantic | 407 | 데이터 구조 정의 및 유효성 검사 라이브러리 |
| &nbsp;&nbsp;↳ annotated-types | 16 | PEP-593 기반 타입 힌트 메타데이터 제공 |
| &nbsp;&nbsp;↳ pydantic-core | 2150 | pydantic의 초고속 핵심 검증 로직 (Rust 구현) |
| &nbsp;&nbsp;↳ typing-extensions | 38 | 구버전 Python을 위한 최신 타입 힌트 백포트 |
| pydantic-settings | 44 | 환경 변수 및 `.env` 기반 애플리케이션 설정 관리 |
| &nbsp;&nbsp;↳ python-dotenv | 24 | `.env` 파일 파싱 유틸리티 |
| typer | 45 | 타입 힌트 기반의 직관적인 CLI 애플리케이션 빌더 |
| &nbsp;&nbsp;↳ click | 98 | 강력한 커맨드 라인 인터페이스(CLI) 생성 도구 |
| loguru | 63 | 설정이 간편하고 강력한 Python 로깅 라이브러리 |
| croniter | 54 | 크론(Cron) 표현식 파싱 및 스케줄링 반복 계산기 |
| &nbsp;&nbsp;↳ python-dateutil | 228 | 강력한 날짜/시간 포맷 파싱 및 조작 유틸리티 |
| &nbsp;&nbsp;↳ pytz | 505 | 전 세계 시간대(Timezone) 계산 지원 |
| msgpack | 334 | JSON보다 빠르고 작게 압축되는 바이너리 직렬화 포맷 |
| **[2. AI & LLM Providers]** | - | **AI 및 언어 모델 연동** |
| openai | 423 | OpenAI API(ChatGPT 등) 공식 클라이언트 |
| &nbsp;&nbsp;↳ anyio | 93 | 비동기 I/O(asyncio, trio) 호환성 계층 |
| &nbsp;&nbsp;↳ distro | 16 | 운영체제(OS) 배포판 정보 확인 유틸리티 |
| &nbsp;&nbsp;↳ sniffio | 6 | 현재 실행 중인 비동기 프레임워크 감지 |
| &nbsp;&nbsp;↳ tqdm | 79 | 터미널 기반 진행률 표시줄(Progress bar) |
| anthropic | 164 | Anthropic API(Claude 모델 등) 공식 클라이언트 |
| &nbsp;&nbsp;↳ tokenizers | 3150 | 텍스트를 AI 모델 토큰으로 변환하는 초고속 라이브러리 (Rust) |
| tiktoken | 1120 | OpenAI 모델용 고속 BPE 토크나이저 |
| &nbsp;&nbsp;↳ regex | 384 | 표준 `re` 모듈을 대체하는 확장 정규 표현식 라이브러리 |
| **[3. Networking & HTTP Clients]** | - | **네트워크 및 HTTP 통신** |
| httpx | 74 | 차세대 동기/비동기 HTTP 클라이언트 (requests 대체재) |
| &nbsp;&nbsp;↳ certifi | 167 | 신뢰할 수 있는 SSL/TLS 인증서 모음 |
| &nbsp;&nbsp;↳ httpcore | 80 | httpx의 하위 레벨 HTTP 코어 구현체 |
| &nbsp;&nbsp;↳ idna | 60 | 국제화 도메인 이름(IDNA) 인코딩/디코딩 지원 |
| websockets | 154 | asyncio 기반의 고성능 WebSocket 서버 및 클라이언트 |
| websocket-client | 59 | 동기식 기반의 저수준 WebSocket 클라이언트 |
| python-socks[asyncio] | 42 | 동기/비동기 SOCKS 프록시 연결 라이브러리 |
| &nbsp;&nbsp;↳ async-timeout | 14 | 비동기 작업에 대한 타임아웃 컨텍스트 관리 |
| socksio | 24 | SOCKS4/SOCKS5 프로토콜 데이터 처리 (Sans-I/O 기반) |
| **[4. Messaging & Chat Channels]** | - | **메신저 채널 연동** |
| python-telegram-bot | 621 | 텔레그램 봇 API와 상호작용하기 위한 래퍼 라이브러리 |
| &nbsp;&nbsp;↳ cryptography | 4250 | 암호화 텍스트 처리 및 보안 프리미티브 제공 |
| slack-sdk | 325 | Slack API, Webhook 등을 다루는 공식 SDK |
| slackify-markdown | 12 | 일반 마크다운 문서를 Slack 전용 포맷으로 변환 |
| qq-botpy | 78 | 텐센트 QQ 메신저 봇 API 클라이언트 |
| &nbsp;&nbsp;↳ aiohttp | 1150 | 비동기 기반의 HTTP 클라이언트 및 서버 프레임워크 |
| &nbsp;&nbsp;↳ pyyaml | 185 | YAML 데이터 파싱 및 생성 라이브러리 |
| lark-oapi | 380 | Feishu(Lark) 오픈 API 공식 연동 SDK |
| &nbsp;&nbsp;↳ requests-toolbelt | 55 | `requests` 라이브러리의 고급 기능 확장 유틸리티 |
| &nbsp;&nbsp;↳ requests | 65 | 가장 널리 쓰이는 표준 동기식 HTTP 클라이언트 |
| dingtalk-stream | 22 | 딩톡(DingTalk) 스트림 API 연결 클라이언트 |
| python-socketio | 80 | 실시간 양방향 통신을 위한 Socket.IO 구현체 |
| &nbsp;&nbsp;↳ bidict | 35 | 키와 값이 1:1로 매칭되는 양방향 사전 자료구조 |
| &nbsp;&nbsp;↳ python-engineio | 60 | Socket.IO의 하위 전송 계층(Engine.IO) 구현체 |
| &nbsp;&nbsp;&nbsp;&nbsp;↳ simple-websocket | 14 | 단순하고 가벼운 WebSocket 서버/클라이언트 |
| **[5. Tools & Protocols]** | - | **검색 도구 및 프로토콜 파싱** |
| ddgs | 45 | DuckDuckGo 검색 엔진 비공식 API 래퍼 (웹 검색용) |
| &nbsp;&nbsp;↳ curl-cffi | 12450 | 브라우저 TLS 지문(Impersonation)을 모방하는 HTTP 클라이언트 |
| &nbsp;&nbsp;↳ lxml | 5320 | C언어 기반의 초고속 XML/HTML 파싱 라이브러리 |
| mcp | 45 | Model Context Protocol 연동을 위한 파이썬 SDK |
| readability-lxml | 42 | 웹 페이지에서 불필요한 요소를 제거하고 본문만 추출 |
| &nbsp;&nbsp;↳ chardet | 202 | 바이트 데이터의 문자열 인코딩 자동 감지 |
| &nbsp;&nbsp;↳ cssselect | 19 | CSS 선택자를 XPath로 변환하여 lxml 검색 지원 |
| json-repair | 36 | LLM이 생성한 불완전하거나 깨진 JSON을 자동으로 복구 |
| oauth-cli-kit | 14 | 터미널 CLI 환경에서의 OAuth 인증 플로우 지원 도구 |
| **[6. CLI Interface & Terminal]** | - | **터미널 UI(TUI) 및 화면 출력** |
| rich | 245 | 터미널에 색상, 표, 프로그레스 바 등 화려한 UI를 렌더링 |
| &nbsp;&nbsp;↳ markdown-it-py | 86 | 마크다운 문서를 Python 객체로 파싱 |
| &nbsp;&nbsp;↳ pygments | 1250 | 소스 코드 구문 강조(Syntax highlighting) 엔진 |
| prompt-toolkit | 392 | 자동 완성, 히스토리 등 강력한 대화형 커맨드 라인 빌더 |
| &nbsp;&nbsp;↳ wcwidth | 35 | CJK(한중일) 등 터미널 내 다국어 문자 폭 계산 |
| questionary | 42 | 터미널에서 선택지, 체크박스 등 대화형 프롬프트 제공 |
| **[7. Optional Dependencies]** | - | **선택적 환경 구성 (수동 설치 필요)** |
| wecom | 200 | 기업용 위챗(WeChat Work) 연동 패키지 묶음 |
| weixin | 15 | 일반 위챗(WeChat) 로그인 및 메시지 연동 묶음 |
| &nbsp;&nbsp;↳ qrcode[pil] | 40 | QR 코드 이미지 생성기 (Pillow 기반) |
| &nbsp;&nbsp;↳ pycryptodome | 14850 | 외부 의존성 없는 자체 완결형 고급 암호화 모듈 |
| matrix | 30 | Matrix(탈중앙화 메신저) 연동 묶음 |
| &nbsp;&nbsp;↳ matrix-nio[e2e] | 215 | 종단간 암호화(E2EE)를 지원하는 Matrix 클라이언트 |
| &nbsp;&nbsp;↳ mistune | 310 | 빠르고 안전하게 마크다운을 HTML로 렌더링 |
| &nbsp;&nbsp;↳ nh3 | 2010 | 악의적인 스크립트 실행을 막기 위한 HTML 살균 도구 (Rust) |
| langsmith | 180 | LangChain 생태계의 LLM 로깅 및 디버깅 플랫폼 클라이언트 |
| dev | 15 | 개발 및 테스트용 패키지 묶음 |
| &nbsp;&nbsp;↳ pytest | 320 | 가장 널리 사용되는 Python 표준 테스트 프레임워크 |
| &nbsp;&nbsp;↳ pytest-asyncio | 45 | 비동기(async) 함수에 대한 단위 테스트 지원 플러그인 |
| &nbsp;&nbsp;↳ pytest-cov | 60 | 소스 코드의 테스트 커버리지 측정 도구 |
| &nbsp;&nbsp;↳ ruff | 30210 | 기존 린터들을 대체하는 초고속 정적 분석 및 포매터 (Rust) |
