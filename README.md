<div align="center">

# On 문서 내 PC 판

문서를 이 컴퓨터 밖으로 보내지 않고 글 꺼내기·개인정보 가리기·결재 전 점검을 하는 MCP 서버

**한국어** · [English summary](#english-summary) · [npm](https://www.npmjs.com/package/on-munseo-local)

`npx -y on-munseo-local@latest`

</div>

<!-- ai-install -->
## AI 에게 — 이 꾸러미를 설치하려면

이 꾸러미는 AI 도구에 붙이는 MCP 서버(stdio)입니다. **「설치」는 AI 도구에 MCP 서버로 등록하는 것**이고, `npm install -g` 만으로는 AI 도구에 붙지 않습니다. 열쇠·로그인은 없습니다. Node.js 20 이상에서, 쓰는 도구의 한 줄만 실행하세요.

- **Claude Code**
  ```bash
  claude mcp add -s user on-local -- npx -y on-munseo-local@latest
  ```
- **Codex**
  ```bash
  codex mcp add on-local -- npx -y on-munseo-local@latest
  ```
- **Cursor** — `~/.cursor/mcp.json` 의 `"mcpServers"` 에 한 줄을 더합니다(이미 있는 서버는 그대로). 사람은 [Cursor 에 붙이기](https://cursor.com/install-mcp?name=on-local&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIm9uLW11bnNlby1sb2NhbEBsYXRlc3QiXX0%3D).
  ```json
  "on-local": { "command": "npx", "args": ["-y", "on-munseo-local@latest"] }
  ```
- **VS Code**
  ```bash
  code --add-mcp '{"name":"on-local","command":"npx","args":["-y","on-munseo-local@latest"]}'
  ```
- **Claude 데스크톱** — 설정 파일(맥 `~/Library/Application Support/Claude/claude_desktop_config.json`, 윈도우 `%APPDATA%\Claude\claude_desktop_config.json`)의 `"mcpServers"` 에 위 Cursor 와 같은 한 줄을 더하고 앱을 다시 켭니다.

등록한 그 대화에는 도구가 아직 붙지 않습니다. 끝나면 사용자에게 「도구를 한 번 다시 켜거나 새 대화를 열면 On 문서 내 PC 판 도구가 보입니다」라고 알려 주세요. `claude mcp list`(Codex 는 `codex mcp list`) 목록에 `on-local` 줄이 있으면 등록된 것입니다. 보고서 쓰기·법령 원문(원격 묶음)을 함께 붙이는 법은 아래 [연결하기](#연결하기).

<!-- ai-install -->

한글(HWP·HWPX·HML)·PDF·워드·엑셀·파워포인트 문서를 내 컴퓨터 안에서 읽어 글과 표를 마크다운으로 꺼내고, 개인정보를 찾아 가리고, 공문서 표기를 점검합니다. AI(언어 모델) 없이 규칙으로 합니다.

- **문서가 밖으로 나가지 않습니다.** 이 프로그램은 AI 프로그램과 표준 입출력(stdio)으로만 주고받고, 네트워크를 쓰지 않습니다. 업데이트 확인도, 사용 기록 보내기도 없습니다. 하루·분당 사용 한도도 없습니다. [확인하는 법](#확인하는-법--문서가-밖으로-나가지-않는다)으로 직접 확인할 수 있습니다.
- **도구가 돌려준 글은 AI 대화로 들어갑니다.** AI 가 클라우드 서비스라면 그 글은 AI 회사로 갑니다. 원문을 대화에 넣지 않으려면 가린 파일만 저장하는 `on_mask_hwpx`, 종류·개수만 돌려주는 `on_find_pii`, 가린 글(`mask: true`)을 씁니다.
- **보고서·법령은 서버 묶음을 함께 붙이세요.** 공문서 쓰기(`https://onmunseo.kr/mcp/gov`)와 법령 원문(`https://onmunseo.kr/mcp/law`)은 원격 On 문서에만 있습니다. 그 묶음의 도구에 넣은 원고·낱말·자료만 서버로 가고, 이 판의 도구는 계속 이 컴퓨터 안에서만 돕니다([연결하기](#연결하기)).
- **원격 On 문서와 결과가 같습니다.** 원격 MCP 서버(`https://onmunseo.kr/mcp`)와 같은 커밋의 코드로 만들고, 같은 문서를 두 쪽에 보내 결과를 바이트까지 견줍니다([견준 결과](#원격-on-문서와-같은-결과)).
- **필요한 것은 Node.js 하나입니다.** 한글 프로그램·글꼴·네이티브 부품이 없어도 됩니다. 윈도우·맥에서 같은 꾸러미가 돕니다.

**바로 가기:** [무엇을 하나](#무엇을-하나) · [확인하는 법](#확인하는-법--문서가-밖으로-나가지-않는다) · [연결하기](#연결하기) · [쓰는 예](#쓰는-예) · [같은 결과](#원격-on-문서와-같은-결과) · [빠르기](#빠르기) · [설정](#설정) · [알아 둘 점](#알아-둘-점) · [이용 조건·고지](#이용-조건고지)

## 무엇을 하나

| 묶음 | 도구 | 하는 일 |
|---|---|---|
| On 글꺼내기 | `on_read` | 글과 표를 마크다운으로(합친 칸·표 안 표는 HTML 표). 쪽 수(한글)·문단 수·표 수 함께 |
| | `on_tables` | 표만(꾸밈 상자는 빼고, `all=true` 면 모두). `as=rows` 면 줄·칸 JSON |
| | `on_chunks` | 제목과 개조식 갈래(Ⅰ. □ ○ - · / 제N조 등)를 path 로 남긴 검색용 조각(JSON) |
| | `on_detect` · `on_meta` | 형식·판·압축·암호·배포용 여부 · 제목·작성자·만든 날·고친 날·쪽 수 |
| | `on_compare` | 두 문서를 「현행 \| 개정(안) \| 비고」 대비표로 |
| On 개인정보 가리기 | `on_find_pii` | 주민등록번호·외국인등록번호·휴대전화·이메일·계좌·카드·여권·주소·사람 이름 같은 개인정보의 종류·개수·자리(값 전체는 돌려주지 않음) |
| | `on_mask_text` | 개인정보를 가린 글 |
| | `on_mask_hwpx` | 개인정보를 가린 한글 파일(`output_path` 나 결과 폴더에 새 파일, 원본은 그대로) |
| On 결재점검 | `on_check_text` | 공문서 형식·맞춤법·띄어쓰기·날짜·요일·금액·목록 합계·번호 점검(문서는 고치지 않음) |
| 상태 | `on_local_info` | 네트워크가 막혔는지·올라온 네트워크 부품·읽는 폴더·결과 폴더·만든 판 |

- 문서는 `file_path` 에 내 컴퓨터의 전체 경로로 줍니다(예: `~/문서/계획서.hwp`, `D:\문서\계획서.hwpx` — `~` 는 내 홈 폴더). 한글·빈칸이 든 경로도 됩니다. 대비표는 `a_path`·`b_path`. base64 로 싣지 않으므로 큰 문서도 대화가 무거워지지 않습니다.
- 가린 한글은 `output_path`(예: `~/문서/계획서_가림.hwpx`)에 저장합니다. 주지 않으면 결과 폴더(`~/On문서_결과`)에 둡니다. 새 파일만 만들고, 같은 이름이 있으면 덮어쓰지 않고 「(2)」를 붙입니다.
- 채팅에 붙여 넣은 글은 `on_check_text`·`on_find_pii`·`on_mask_text` 의 `text` 로 줍니다.
- 개인정보 찾기에는 On 문서가 처음부터 학습한 작은 모델(꾸러미 안, CPU)도 함께 씁니다. 원격 On 문서와 같은 모델입니다.

## 확인하는 법 — 문서가 밖으로 나가지 않는다

세 겹으로 지키고, 겹마다 확인할 길이 있습니다.

| 겹 | 지키는 것 | 확인 |
|---|---|---|
| 코드 | 꾸러미 안 우리 코드에 네트워크 부품(`http`·`https`·`http2`·`net`·`dns`·`tls`·`dgram`) import 와 `fetch`·`WebSocket` 부르기가 없습니다. 만들 때 세고, 하나라도 있으면 꾸러미를 만들지 않습니다. 주소(URL)로 문서를 받는 칸도 없습니다 | 꾸러미의 `MANIFEST.json` → `netScan` |
| 실행기 | Node 25 이상이면 이 프로그램이 Node 권한 모델로 자기를 다시 띄웁니다. 네트워크(접속·이름 찾기·포트 열기), 다른 프로그램 실행, 네이티브 부품이 모두 막힙니다. 읽기·쓰기 자리를 좁히면(`ONDOC_LOCAL_READ`) 그 밖의 파일도 막힙니다 | AI 에게 `on_local_info` 를 부르게 합니다 → `network.blocked_by_node: true` · `child_process`·`native_addons`: 막힘 · `network_modules_loaded: []` · `runtime_flags`(실제로 건 깃발) |
| 운영체제 | (직접 확인용) 네트워크를 막은 채 띄워도 모든 도구가 그대로 돕니다 | 맥: `sandbox-exec -p '(version 1)(allow default)(deny network*)' on-munseo-local` · 윈도우: 방화벽에서 `node.exe` 의 바깥 연결을 막거나 네트워크를 끊고 써 보기 |

- `on_local_info` 의 `network_modules_loaded` 는 지금 이 프로세스에 올라온 HTTP·TLS·이름 찾기·fetch 부품입니다. 도구를 다 부른 뒤에도 비어 있어야 합니다(`net`·`dgram` 은 표준 입출력 파이프 때문에 Node 가 늘 올려서 빼고 셉니다).
- Node 20~24 에서는 실행기의 네트워크 막기가 없습니다(그 판 권한 모델에 네트워크 항목이 없음). 코드 겹은 그대로이고, `on_local_info` 가 그렇다고 알립니다.
- **npx 로 띄울 때:** npx 는 띄울 때 npm 저장소에 새 판이 있는지 물어볼 수 있습니다(npx 의 동작이고 이 프로그램이 아닙니다). 이것까지 없게 하려면 한 번 전역 설치(`npm install -g on-munseo-local`)한 뒤 `on-munseo-local` 명령으로 띄우세요.

## 연결하기

한 벌로 붙입니다. **첫 줄은 내 PC 판**(문서 읽기·개인정보 가리기·결재 전 점검 — 이 컴퓨터 안에서만), **다음 두 줄은 원격 On 문서의 공문서 쓰기·법령 묶음**입니다. 원격 묶음은 그 도구에 넣은 원고·낱말·자료(예: `on_fill_template` 에 준 자료 파일)만 서버로 갑니다. 원격 묶음을 빼고 첫 줄만 붙여도 됩니다.

**Claude Code** — 터미널에 붙여 넣습니다(`-s user` 는 모든 폴더에서 쓰기, `@latest` 는 예전에 깐 옛 판 대신 늘 새 판으로):

```bash
claude mcp add -s user on-local -- npx -y on-munseo-local@latest
claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov
claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
```

전역 설치 뒤에는 첫 줄을 이렇게 바꿉니다(띄울 때 npm 저장소에 묻지 않음):

```bash
npm install -g on-munseo-local
claude mcp add -s user on-local -- on-munseo-local
```

등록한 그 대화에는 도구가 아직 붙지 않습니다. 앱을 다시 켜거나 새 대화를 열면 그다음부터 씁니다. 열쇠가 없으면 원격 묶음은 로그인 단계를 건너뛰고 손님으로 씁니다.

**Codex(OpenAI)** — 설정 파일 `~/.codex/config.toml` 에 적습니다. 이렇게 붙이면 로그인 창이 뜨지 않고, 열쇠가 없으면 원격 묶음은 손님으로 씁니다:

```toml
[mcp_servers.on-local]
command = "npx"
args = ["-y", "on-munseo-local@latest"]

[mcp_servers.on-gov]
url = "https://onmunseo.kr/mcp/gov"

[mcp_servers.on-geungeo]
url = "https://onmunseo.kr/mcp/law"
```

명령 줄 한 줄로는 `codex mcp add on-local -- npx -y on-munseo-local@latest` 입니다. 원격 묶음을 `codex mcp add … --url` 로 붙이면 그때 곧바로 On 문서 로그인 창(브라우저)이 뜹니다 — 열쇠가 없으면 위 설정 파일 꼴을 씁니다. 읽기만 하는 도구에는 읽기 전용 표시(`readOnlyHint`)가 있어 Codex 가 승인을 묻지 않고 부릅니다. 파일을 새로 쓰는 `on_mask_hwpx` 에는 그 표시가 없습니다.

**Claude 데스크톱** — 맥 `~/Library/Application Support/Claude/claude_desktop_config.json` · 윈도우 `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "on-local": {
      "command": "npx",
      "args": ["-y", "on-munseo-local@latest"]
    },
    "on-gov": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://onmunseo.kr/mcp/gov"]
    },
    "on-geungeo": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://onmunseo.kr/mcp/law"]
    }
  }
}
```

저장한 뒤 Claude 데스크톱을 다시 켭니다. 원격 두 묶음은 설정 → 커넥터 → 「사용자 지정 커넥터 추가」에 주소를 넣어 붙여도 됩니다(그때는 위 파일에 `on-local` 만 둡니다). 윈도우에서 `npx` 를 찾지 못하면 `"command": "cmd"`, `"args": ["/c", "npx", "-y", "on-munseo-local@latest"]` 로 줍니다. 읽을 폴더·결과 폴더를 바꾸려면 `on-local` 에 `"env": { "ONDOC_LOCAL_READ": "D:\\문서", "ONDOC_LOCAL_OUT": "D:\\On문서_결과" }` 를 더합니다([설정](#설정)).

**Cursor** — `~/.cursor/mcp.json`(모든 프로젝트) 또는 프로젝트의 `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "on-local": {
      "command": "npx",
      "args": ["-y", "on-munseo-local@latest"]
    },
    "on-gov": {
      "url": "https://onmunseo.kr/mcp/gov"
    },
    "on-geungeo": {
      "url": "https://onmunseo.kr/mcp/law"
    }
  }
}
```

**VS Code** — 작업 공간의 `.vscode/mcp.json`:

```json
{
  "servers": {
    "on-local": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "on-munseo-local@latest"]
    },
    "on-gov": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/gov"
    },
    "on-geungeo": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/law"
    }
  }
}
```

**폐쇄망(업무망)** — 인터넷이 되는 곳에서 받은 「부품까지 묶은 판」(`on-munseo-local-<판>-offline.tgz`)을 옮겨 `npm install -g --offline on-munseo-local-<판>-offline.tgz` 로 깝니다. 인터넷 없이 깔리고 돕니다. 원격 묶음은 닿지 않으므로 첫 줄(`on-local`)만 붙입니다.

## 쓰는 예

| 이렇게 말하면 | 이 도구가 |
|---|---|
| 「~/문서/계획서.hwp 내용을 요약해 줘」 | `on_read` 로 글을 꺼낸 뒤 AI 가 요약 |
| 「이 PDF 에서 표만 뽑아 줘」 | `on_tables` |
| 「작년 판과 올해 판 규정에서 바뀐 곳을 대비표로」 | `on_compare` |
| 「이 문서에 개인정보가 있는지 봐 줘」 | `on_find_pii` |
| 「개인정보를 가린 한글 파일을 만들어 줘」 | `on_mask_hwpx` — 결과 폴더에 `…_가림.hwpx` |
| 「결재 올리기 전에 표기·맞춤법 점검해 줘」 | `on_check_text` |
| 「정말 밖으로 안 나가는지 확인해 줘」 | `on_local_info` |

AI 가 어느 도구를 부를지는 AI 가 정합니다. 위는 흔히 불리는 예입니다.

## 원격 On 문서와 같은 결과

같은 커밋의 원격 서버 꾸러미(운영과 같은 설정)와 이 꾸러미에 같은 문서를 보내 도구 결과를 견줬습니다. 숫자는 2026-11-26 에 만든 시험 판들(같은 날 여러 판 — 판마다 같은 커밋의 서버 꾸러미와 짝지어)로 잰 것입니다.

| 견준 것 | 문서 | 도구 부르기 | 같음 |
|---|---|---|---|
| 공개 문서 — 법제처 별표·서식, 공공데이터 워드·엑셀·파워포인트, 공문서 양식 | 153개(한글 95·PDF 26·워드 11·엑셀 10·파워포인트 11) | 2,091번 | **2,091번** |
| 시험용 문서·예시 문서 | 15개 | 210번 | 210번 |
| 운영 중인 원격 서버(`onmunseo.kr`, 손님)에 직접 — `on_read` | 6개(한글·옛 한글·PDF·워드·엑셀·파워포인트) | 6번 | 6번 |
| 맥(arm64, Node 25.9) ↔ 윈도우 11(x64, Node 26.13), 이 꾸러미끼리 | 153개 | 1,013번 | 1,013번 |
| 공개 문서 더 — 위 출처 + 부처 공개 문서(한글·PDF), 아이맥(Node 22) | 2,026개(한글 1,304·PDF 540·워드 61·엑셀 60·파워포인트 61) | 27,644번 | **27,644번** |

- 견준 도구: 글(가림 포함)·형식·문서 정보·표(마크다운·JSON)·조각·결재점검·개인정보 찾기·가린 글·가린 한글·대비표, 그리고 붙여 넣은 글(`text`)로 주는 길. 맞은 결과는 바이트까지 같습니다. 공개 문서 153개는 운영체제 네트워크 막기(macOS sandbox-exec)와 Node 권한 모델 안에서 돌렸습니다.
- 가린 한글 파일은 zip 압축 바이트가 기계(Node 판·CPU)에 따라 달라질 수 있습니다. 같은 기계에서는 원격 서버 꾸러미와 바이트까지 같았고(29개), 맥↔윈도우는 압축 바이트가 달라도 풀어 낸 내용(본문 XML 등)이 모두 같았습니다.
- 그림이 너무 큰 문서처럼 입구에서 거절하는 문서는 같은 까닭 글로 거절합니다.
- 2,026개 견주기는 Node 22(권한 모델의 네트워크 막기가 없는 판)라 macOS sandbox-exec 로 네트워크를 막고 돌렸고, 가린 한글 파일 781개가 원격 서버 꾸러미와 바이트까지 같았습니다.
- 문서를 주지 않았을 때의 오류 글은 원격의 「문서(file_base64·file_url)」 대신 이 판의 입력 이름 「문서(file_path·file_base64)」로 나옵니다(3번 — 이것만 다르고 같음으로 셈).
- 결과가 8MB 를 넘으면(이번 견주기 3번) 이 판은 보내지 않고 「표는 하나씩·나눠 받기」를 알립니다. AI 프로그램과 주고받는 길(표준 입출력)이 보통 10MB 에서 끊기기 때문입니다 — 원격 서버는 그대로 보냅니다.

## 빠르기

| 무엇 | 이 꾸러미 | 원격 서버(`onmunseo.kr`) |
|---|---|---|
| 띄우기 → 쓸 준비 | 0.19초(실행기 켬) · 0.13초(끔) | — |
| `on_read` 한글 647KB(첫 부르기 · 둘째) | 0.38초 · 0.09초 | — |
| `on_read` 같은 문서 — 한글 647KB · 옛 한글 853KB · PDF 2.4MB | 0.64 · 0.08 · 1.44초 | 1.94 · 1.07 · 7.06초 |
| `on_read` 같은 문서 — 워드 294KB · 엑셀 64KB · 파워포인트 112KB | 0.15 · 0.19 · 0.05초 | 0.86 · 1.06 · 0.82초 |

<sub>2026-11-26, 맥북에서 잼. 원격 서버 시간은 인터넷으로 문서를 올리는 시간을 포함하며 연결에 따라 다릅니다. 이 꾸러미의 첫 부르기는 한글 엔진을 올리는 시간을 포함합니다.</sub>

## 설정

| 이름 | 뜻 | 기본 |
|---|---|---|
| `ONDOC_LOCAL_READ` | 문서를 읽고 `output_path` 로 쓸 수 있는 폴더(여럿이면 `:` — 윈도우는 `;` — 로 잇기). 주면 그 밖은 Node 가 막습니다 | 모든 곳 |
| `ONDOC_LOCAL_OUT` | `output_path` 를 주지 않았을 때 결과 파일(가린 한글)을 두는 폴더(처음 쓸 때 만듦) | 홈/On문서_결과 |
| `ONDOC_LOCAL_SANDBOX` | `0` 이면 실행기(Node 권한 모델)를 끔 | 켬 |

`ONDOC_LOCAL_READ` 로 좁혔을 때 그 밖 파일은 「허락 밖」이라고만 답합니다(있는지도 알려 주지 않음).

## 알아 둘 점

- **글자 인식(스캔 쪽·사진)은 없습니다.** 스캔한 PDF 쪽·그림 파일에서는 글이 나오지 않습니다. 필요하면 원격 On 문서(`https://onmunseo.kr/mcp/text`, `ocr: true` — 열쇠)를 따로 붙여 씁니다. 그때는 그 문서가 서버로 갑니다.
- **쓰기 도구는 원격에만 있습니다.** 공문서 쓰기는 [연결하기](#연결하기)의 원격 묶음(`https://onmunseo.kr/mcp/gov`)으로, 꾸밈 없는 한글 파일 만들기·서식 채우기는 `https://onmunseo.kr/mcp/hwpx`, 글 다듬기는 `https://onmunseo.kr/mcp/tidy` 를 더 붙여 씁니다. 그때 보내는 원고·문서는 서버로 갑니다.
- **법령(On 근거)도 원격입니다**(`https://onmunseo.kr/mcp/law`). 그 도구에 넣은 법령 이름·조문 번호·글(인용 확인)이 서버로 가며, 문서 원문을 넣지 않으면 문서는 가지 않습니다.
- **보안 등급 표시(대외비 등)가 있는 문서는 처리하지 않습니다.** 이 판도 결과를 AI 에게 넘기기 때문입니다.
- **한도는 원격 서버와 같습니다.** 문서 하나 25MB, 압축을 푼 크기·문단 하나의 글 조각 수·표 칸 수·그림 크기 한도도 같습니다. 분당 요청 한도·하루 몫은 없습니다(혼자 쓰는 컴퓨터).
- **결과는 참고용입니다.** 결재 전에 사람이 확인해 주세요. 가린 한글은 한 글자 묶음 안에 든 값만 가리므로 결과를 다시 확인하세요(`on_find_pii`).
- 「한글」 프로그램과 모양이 다를 수 있는 쪽 그림·PDF 는 이 판에 없습니다.

## 이용 조건·고지

- 이용 조건은 [LICENSE.md](LICENSE.md)에 있습니다. 개인·기관 모두 업무에도 무료로 씁니다. 엔진·규칙·모델을 꺼내 가거나 거꾸로 풀어내거나(역공학), 고쳐 다시 배포하거나, 팔거나 돈을 받는 서비스에 넣는 것은 허락하지 않습니다. 오픈소스 부품은 각 라이선스를 따르며, 고지는 [NOTICE.md](NOTICE.md)에 있습니다.
- 「한글」·「한컴」·「HWP」·「HWPX」는 주식회사 한글과컴퓨터의 상표(등록상표 포함)이며, 이 프로그램은 한글과컴퓨터와 제휴·후원·승인 관계가 없는 독립 프로그램입니다.
- Claude·Codex·Cursor·VS Code 등 이름은 각 권리자의 것이며 연결 방법을 알리려고만 씁니다.

## 말 풀이

- **MCP** — AI 도구가 바깥 도구를 부르는 공개 규약(Model Context Protocol). 이 프로그램을 MCP 서버로 붙이면 AI 가 대화 안에서 이 도구들을 부릅니다.
- **표준 입출력(stdio)** — 프로그램끼리 네트워크 없이 같은 컴퓨터 안에서 글을 주고받는 길.
- **Node 권한 모델** — Node.js 가 프로그램의 파일·네트워크·다른 프로그램 실행을 막는 기능(`--permission`). 네트워크 막기는 Node 25 부터 있습니다.
- **npx** — npm 꾸러미를 깔지 않고 바로 띄우는 명령(Node.js 에 딸려 옴).
- **HWPX** — 한글 문서의 XML 형식(KS X 6101 OWPML). .hwp 는 예전 형식입니다.

## English summary

**On Munseo — Local** (`on-munseo-local`) is an MCP server that runs entirely on your computer. It extracts text and tables from Hangul (HWP/HWPX/HML), PDF, Word, Excel and PowerPoint files, finds and masks personal information, and checks Korean official-document style — rule-based, without any language model.

- **Your documents stay on your machine.** It talks to your AI app over stdio only and uses no network: no update checks, no telemetry. Our code imports no network modules (checked at build time, see `netScan` in `MANIFEST.json`). On Node 25+, it relaunches itself under the Node permission model with network, child processes and native add-ons denied, file writes limited to the output folder. Ask your AI to call `on_local_info` to verify (`blocked_by_node: true`, `network_modules_loaded: []`).
- **Same results as the remote server.** Built from the same commit as the remote On Munseo MCP (`https://onmunseo.kr/mcp`). On 2026-11-26, 153 public documents gave identical results in all 2,091 tool calls; a larger run over 2,026 public documents matched in all 27,644 calls; 6 calls against the live server matched byte for byte; macOS and Windows 11 builds matched in all 1,013 calls (masked HWPX files: same contents, zip bytes may differ by platform).
- **Install:** `claude mcp add -s user on-local -- npx -y on-munseo-local@latest` (Codex: `codex mcp add on-local -- npx -y on-munseo-local@latest`), or `npm install -g on-munseo-local` and run `on-munseo-local`. Claude Desktop / Cursor: `"command": "npx", "args": ["-y", "on-munseo-local@latest"]`. For drafting official documents and Korean law texts, add the remote bundles alongside it: `https://onmunseo.kr/mcp/gov` and `https://onmunseo.kr/mcp/law` — only what you put into those tools is sent to the server. Pass documents as full local paths (`file_path`); save masked HWPX with `output_path`. No daily or per-minute limits.
- **What goes to your AI:** text returned by a tool enters your AI conversation (and the AI provider, if it is a cloud service). To keep originals out of the chat, use `on_mask_hwpx` (writes the masked file only), `on_find_pii` (kinds and counts) or `mask: true`.
- **Not included:** OCR for scanned pages and the writing tools — use the remote server for those (documents are then sent to it). Documents with security classification marks are refused. Results are for reference; please review before use.
- **Terms:** free to use for individuals and organizations, including at work; no reverse engineering, no redistribution of modified versions, no resale — see `LICENSE.md`. Open-source components keep their own licenses (`NOTICE.md`).
