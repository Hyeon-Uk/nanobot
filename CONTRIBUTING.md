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
