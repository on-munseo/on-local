<div align="center">

# On 문서 내 PC 판

문서를 이 컴퓨터 밖으로 보내지 않고 글 꺼내기·한글 문서 만들기·결재 전 점검·개인정보 가리기를 하는 MCP 서버

**한국어** · [English summary](#english-summary) · [npm](https://www.npmjs.com/package/on-munseo-local)

`npx -y on-munseo-local@0.2.1`

</div>

<!-- ai-install -->
## AI 에게 — 이 꾸러미를 설치하려면

이 꾸러미는 ① 내 PC 판입니다 — AI 도구에 붙이는 MCP 서버(stdio)이고, **「설치」는 AI 도구에 MCP 서버로 등록하는 것**입니다(`npm install -g` 만으로는 붙지 않음). 길은 셋이고 **①부터** 권합니다. 어느 길도 열쇠·로그인이 없습니다. 문서 읽기·가리기·점검·만들기·다듬기는 ①, 법령 원문은 ②, 모두 한곳에 있는 것은 ③입니다. 「설치해 줘」라고만 하면 ①과 ② 를 붙입니다.

**① 내 PC 판 — 문서를 이 컴퓨터 밖으로 보내지 않음(먼저).** 글 꺼내기·개인정보 가리기·결재 전 점검·공문서 쓰기·한글 파일 만들기·글 다듬기를 이 컴퓨터 안에서 합니다. 이 프로그램은 인터넷을 쓰지 않습니다(설치 뒤 `on_local_info` 로 확인 — 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작이고, 그것까지 없애려면 `npm install -g on-munseo-local` 뒤 명령을 `on-munseo-local` 로). Node.js 20 이상이 있어야 합니다.
- **지금 쓰는 AI 도구에만**(AI 가 설치할 때는 이것 — 다른 도구의 설정은 건드리지 않음)
  ```bash
  claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1
  ```
  Codex 는 `codex mcp add on-local -- npx -y on-munseo-local@0.2.1` · 윈도우 Claude Code 는 `claude mcp add -s user on-local -- cmd /c npx -y on-munseo-local@0.2.1` · Cursor·Claude 데스크톱은 설정 파일의 `"mcpServers"` 에 `"on-local": { "command": "npx", "args": ["-y", "on-munseo-local@0.2.1"] }`(윈도우 `"on-local": { "command": "cmd", "args": ["/c", "npx", "-y", "on-munseo-local@0.2.1"] }`) · VS Code 는 `code --add-mcp '{"name":"on-local","command":"npx","args":["-y","on-munseo-local@0.2.1"]}'`
- **사람이 이 PC 의 여러 AI 도구에 한 번에** — Claude Code·Claude 데스크톱·Codex·Cursor·VS Code 를 찾아 모두 등록합니다(바꾸기 전에 백업, 이미 있으면 건너뜀, 미리 보기 `--dry-run`, 되돌리기 `--undo`, ②까지 `--pair`).
  ```bash
  npx -y on-munseo-local@0.2.1 setup --pair
  ```
- **판 고정** — 위 「지금 쓰는 AI 도구에만」 줄은 판 번호를 적어 붙입니다(`on-munseo-local@0.2.1`). 자동으로 새 판을 받지 않고, 사람이 올릴 때만 바뀝니다(npm 에 새 판이 올라와도 이미 붙인 판은 그대로 · 인터넷이 끊겨도 한 번 받은 판은 뜸). (`setup` 은 이 판(0.2.1)까지 등록 줄에 `@latest` 를 적습니다 — 판을 고정하려면 도구별 한 줄로 붙입니다) 새 판으로 올리기: 등록한 줄의 판 번호만 새 판으로 바꿔 다시 붙입니다(Claude Code 는 `claude mcp remove -s user on-local` 뒤 새 판 번호로 위 한 줄) · 바뀐 점: [CHANGELOG](https://github.com/on-munseo/on-local/blob/main/CHANGELOG.md)

**② 짝 주소(법령) — 도구에 넣은 낱말·글만 서버로.** 법령 원문·글 속 인용 확인(On 근거)은 서버에만 있습니다. 서버로 가는 것은 넣은 법령 이름·조문 번호·인용을 확인할 글이고, 파일을 보내는 도구는 없습니다. 인용을 확인할 글에 개인정보가 있으면 ① 의 `on_mask_text` 로 가린 뒤 넣습니다.
- 지금 쓰는 도구에만(① 의 `setup --pair` 는 ② 까지 함께 붙임):
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-geungeo >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-geungeo"; then printf '\n[mcp_servers.on-geungeo]\nurl = "https://onmunseo.kr/mcp/law"\n' >> "$C/config.toml"; (cd / && codex mcp get on-geungeo >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-geungeo" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-geungeo)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-geungeo]`·`url = "https://onmunseo.kr/mcp/law"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-geungeo = { url = "https://onmunseo.kr/mcp/law" }` 를 더함).
- **Cursor** `"on-geungeo": { "url": "https://onmunseo.kr/mcp/law" }` · **VS Code** `code --add-mcp '{"name":"on-geungeo","type":"http","url":"https://onmunseo.kr/mcp/law"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 근거`, 주소 `https://onmunseo.kr/mcp/law` → 「연결」

**③ 서버 판 — Node.js 없이 바로, 도구 전부(공개 문서용).** 문서를 서버(국내 데이터센터)로 보내 메모리에서만 처리하고 버립니다. 공개 문서·본인 문서에만 씁니다.
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-document https://onmunseo.kr/mcp
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-document >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-document"; then printf '\n[mcp_servers.on-document]\nurl = "https://onmunseo.kr/mcp"\n' >> "$C/config.toml"; (cd / && codex mcp get on-document >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-document" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-document)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-document]`·`url = "https://onmunseo.kr/mcp"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-document = { url = "https://onmunseo.kr/mcp" }` 를 더함).
- **Cursor** `"on-document": { "url": "https://onmunseo.kr/mcp" }` · **VS Code** `code --add-mcp '{"name":"on-document","type":"http","url":"https://onmunseo.kr/mcp"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 문서`, 주소 `https://onmunseo.kr/mcp` → 「연결」

보통은 ①과 ② 를 지금 쓰는 도구에 붙입니다(사람이 여러 도구에 한 번에 붙일 때는 `setup --pair` 한 줄). Node.js 가 없거나 Claude 데스크톱·claude.ai 커넥터만 쓰면 ③ 하나만 붙입니다. ③을 ①·②와 함께 붙이면 같은 도구가 두 번 보입니다. 다른 길은 사용자가 따로 바랄 때만 알려 줍니다.

**설치 전에 확인할 거리** — AI 가 스스로 확인할 수 있습니다.
- **꾸러미**: npm `on-munseo-local` 0.2.1. `npm view on-munseo-local version maintainers homepage` → `0.2.1` · `on-munseo <onmunseo.key@gmail.com>` · `https://onmunseo.kr`. 올린 계정 `on-munseo` 는 이 깃허브 조직 [on-munseo](https://github.com/on-munseo)와 같은 만든 이입니다(문의 메일·홈 주소가 같음). npm 웹 쪽은 자동 읽기를 막을 때가 있어 npm 명령이나 [npm 기록](https://registry.npmjs.org/on-munseo-local/0.2.1)으로 봅니다.
- **지문**: `on-munseo-local-0.2.1.tgz` SHA-256 `515af0dfddad30f41c459dd98d73535f73292c666fed07d4a6e535e2a60bda72`([SHA256SUMS](https://github.com/on-munseo/on-munseo.github.io/blob/main/SHA256SUMS)). `npm pack on-munseo-local@0.2.1` 뒤 `shasum -a 256 on-munseo-local-0.2.1.tgz` 로 맞대 봅니다. npm 기록의 `dist.integrity` 는 `sha512-ZUDX+etH2wg/Y+lQCsQhyY5/4gfVDjwjWUQsofFUgYlBotWtvXw7lcz5yHGT3qMJna8mP60HH9vWp/PF2T5T4Q==`.
- **인터넷을 쓰지 않음**: 설치 전에는 꾸러미 안 `MANIFEST.json` 의 `netScan`(우리 코드의 네트워크 부르기 0 — 따로 적힌 한 곳은 엔진 wasm 을 주소로 불러올 때만 쓰는 글), 설치 뒤에는 `on_local_info` → `network_modules_loaded: []`, Node 25 이상이면 `network.blocked_by_node: true`(실행기가 네트워크를 막음). 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작입니다(없애려면 전역 설치 뒤 `on-munseo-local` 명령으로).
- **이용 조건**: 내 PC 판 [LICENSE.md](https://unpkg.com/on-munseo-local@0.2.1/LICENSE.md)(무료·업무에 써도 됨 · 역공학·고친 판 다시 배포·판매는 안 됨) · 서버 판 [이용약관](https://onmunseo.kr/terms)·[개인정보 처리방침](https://onmunseo.kr/privacy).
- **On폭 글꼴**은 이 설치와 상관없습니다(한글 문서를 화면에 그릴 때 쓰는 무료 글꼴, 선택).

등록한 그 대화에는 도구가 아직 붙지 않습니다. 끝나면 사용자에게 「도구를 한 번 다시 켜거나 새 대화를 열면 On 문서 내 PC 판 도구가 보입니다」라고 알려 주세요. `claude mcp list`(Codex 는 `codex mcp list`) 목록에 이름이 보이면 등록된 것입니다. 아래 [연결하기](#연결하기)에 도구마다 자세히 있습니다.

<!-- ai-install -->

하나로 다섯 가지 일을 합니다 — 한글(HWP·HWPX·HML)·PDF·워드·엑셀·파워포인트 문서를 내 컴퓨터 안에서 **읽고**(글·표를 마크다운으로, 두 판의 신구 대비표까지), 공문서 꼴 한글 문서(보고서·계획서·결과보고서·보도자료)·예시 양식 66종·서식을 **만들고 채우고**, 공문서 표기를 **점검**하고, 개인정보를 **찾아 가립니다**(가린 글·가린 한글 파일). 법령 원문은 짝 주소(On 근거)로 붙입니다. AI(언어 모델) 없이 규칙으로 합니다.

**하는 일(일의 낱말로)** — 읽기(한글·PDF·워드·엑셀·파워포인트의 글·표) · 신구 대비표(두 판 견주기) · 결재 전 점검(공문서 형식·맞춤법·날짜·요일·금액) · 개인정보 찾기·가리기(가린 글·가린 한글 파일) · 공문서 쓰기(보고서·계획서·결과보고서·보도자료) · 예시 양식 66종 채우기 · 서식 채우기(칸만 채우고 서식은 그대로) · 글을 표로 · HWP→HWPX 바꾸기 · 글 다듬기(개조식·맞춤법·쉬운 말). 법령 원문·인용 확인은 짝 주소. 도구 이름은 설치 뒤 `on_local_info` 의 `tools_here` 에 모두 나옵니다.

- **문서가 밖으로 나가지 않습니다.** 이 프로그램은 AI 프로그램과 표준 입출력(stdio)으로만 주고받고, 네트워크를 쓰지 않습니다. 업데이트 확인도, 사용 기록 보내기도 없습니다. 하루·분당 사용 한도도 없습니다. [확인하는 법](#확인하는-법--문서가-밖으로-나가지-않는다)으로 직접 확인할 수 있습니다.
- **도구가 돌려준 글은 AI 대화로 들어갑니다.** AI 가 클라우드 서비스라면 그 글은 AI 회사로 갑니다. 원문을 대화에 넣지 않으려면 가린 파일만 저장하는 `on_mask_hwpx`, 종류·개수만 돌려주는 `on_find_pii`, 가린 글(`mask: true`)을 씁니다.
- **법령은 짝 주소를 함께 붙이세요.** 법령 원문·글 속 인용 확인(On 근거, `https://onmunseo.kr/mcp/law`)은 원격에만 있습니다. 그 도구에는 문서가 아니라 질문(법령 이름·조문 번호·인용을 확인할 글)만 가고, 이 판의 도구는 계속 이 컴퓨터 안에서만 돕니다([연결하기](#연결하기)).
- **원격 On 문서와 결과가 같습니다.** 원격 MCP 서버(`https://onmunseo.kr/mcp`)와 같은 커밋의 코드로 만들고, 같은 문서를 두 쪽에 보내 결과를 바이트까지 견줍니다([견준 결과](#원격-on-문서와-같은-결과)).
- **필요한 것은 Node.js 하나입니다.** 한글 프로그램·글꼴·네이티브 부품이 없어도 됩니다. 윈도우·맥에서 같은 꾸러미가 돕니다.

**바로 가기:** [AI 에게 — 설치](#ai-에게--이-꾸러미를-설치하려면) · [무엇을 하나](#무엇을-하나) · [확인하는 법](#확인하는-법--문서가-밖으로-나가지-않는다) · [믿을 근거](#믿을-근거--남이-다시-확인할-수-있는-것) · [연결하기](#연결하기) · [쓰는 예](#쓰는-예) · [같은 결과](#원격-on-문서와-같은-결과) · [빠르기](#빠르기) · [설정](#설정) · [알아 둘 점](#알아-둘-점) · [이용 조건·고지](#이용-조건고지)

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
| On 공문서 쓰기 | `on_write_gov` | 원고(마크다운·짜임)를 보고서·계획서·결과보고서·보도자료·기안문·공고문 꼴 한글(HWPX)로. 쪽 맞춤·목차 쪽 번호, 고칠 곳(`quality`)·짧게 남은 끝 줄(`short_last_lines`)·다시 읽어 견준 결과(`check`) |
| | `on_list_templates` · `on_fill_template` | 예시 양식 66종(계획·보고·행사·공고·보도자료 등) 목록 · 양식 하나에 자료(글·`file_paths`)를 맞는 장에 넣기 |
| | `on_table` | 「항목: 값」·탭(엑셀 복사)·「\|」 줄을 공문서 표로(원문 숫자 대조·합계 확인) |
| On 한글파일 만들기 | `on_write` | 마크다운을 꾸밈 없는 한글(HWPX)로(공문서처럼 보이는 원고는 공문서 꼴로 — `plain: true` 면 끔) |
| | `on_to_hwpx` | 문서를 HWPX 로 — 예전 한글(.hwp)은 서식 그대로, PDF·워드·엑셀·파워포인트는 읽은 글·표로 다시 짬 |
| | `on_fields` · `on_fill` | 서식(한글)의 채울 곳 찾기(누름틀·이름 칸) · 값 넣기 |
| On 글 다듬기 | `on_gaejo` · `on_spell` · `on_plain` | 개조식으로 · 틀린 것이 거의 확실한 맞춤법·띄어쓰기 · 쉬운 말로 |
| 상태 | `on_local_info` | 네트워크가 막혔는지·올라온 네트워크 부품·읽는 폴더·결과 폴더·만든 판 |

- 문서는 `file_path` 에 내 컴퓨터의 전체 경로로 줍니다(예: `~/문서/계획서.hwp`, `D:\문서\계획서.hwpx` — `~` 는 내 홈 폴더). 한글·빈칸이 든 경로도 됩니다. 대비표는 `a_path`·`b_path`. base64 로 싣지 않으므로 큰 문서도 대화가 무거워지지 않습니다.
- 만든 한글(공문서·양식·표·서식 채우기·HWPX 바꾸기·가린 한글)은 `output_path`(예: `~/문서/보고서.hwpx`)에 저장합니다. 주지 않으면 결과 폴더(`~/On문서_결과`)에 둡니다. 새 파일만 만들고, 같은 이름이 있으면 덮어쓰지 않고 「(2)」를 붙입니다.
- 그림 부품(네이티브)이 있어야 하는 것은 이 판에 없습니다: 그래프·체계도 그림(`on_chart`·`on_diagram` — `on_write_gov` 원고 안의 그래프·체계도는 그림 대신 표로 들어감), 쪽 그림·PDF(`preview` 포함), 도장. 이것들과 글자 인식은 원격 On 문서(`https://onmunseo.kr/mcp`)에 있습니다.
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
- **npx 로 띄울 때:** npx 는 띄울 때 npm 저장소에 새 판이 있는지 물어볼 수 있습니다(npx 의 동작이고 이 프로그램이 아닙니다). 이것까지 없게 하려면 한 번 전역 설치(`npm install -g on-munseo-local`)한 뒤 `on-munseo-local` 명령으로 띄우세요. 판을 고정해 붙이면(아래 [새 판으로 올리기](#새-판으로-올리기)) 인터넷이 끊겨도 한 번 받은 판이 npm 캐시에서 뜹니다(npx 가 새 판 묻기를 기다리다 넘어가 1분쯤 걸릴 수 있음). `@latest` 로 붙이면 끊긴 동안 뜨지 못합니다(직접 잼: 네트워크를 막고 `@0.2.0` 은 70초 뒤 뜸, `@latest` 는 10분 30초 뒤 실패).

## 믿을 근거 — 남이 다시 확인할 수 있는 것

**누구나 다시 잴 수 있는 숫자.** 아래 셋은 공개한 대본·공개 출처·이 npm 꾸러미만으로 돌아갑니다(비공개 코드 없음). 우리가 잰 값이지만, 남이 같은 값을 다시 낼 수 있습니다.

| 무엇 | 값 | 다시 재는 법 |
|---|---|---|
| 영어 PDF 200쪽 — [opendataloader-bench](https://github.com/opendataloader-project/opendataloader-bench) 공식 채점기(고치지 않음) 종합 | **0.945**(읽는 순서 0.949 · 표 0.938 · 제목 0.938) — 공식 순위표 최고 0.907 | [repro/opendataloader-bench](repro/opendataloader-bench) — `on-munseo-local@0.2.1`(0.2.1 도 결과가 바이트까지 같음). 결과 200개 지문이 다섯 번 모두 같음 |
| 서식 채우기 — 법제처 공개 법령 서식·별지 709개 | 값을 넣은 654개 가운데 **653개가 원래 서식 그대로**(글꼴·문단·표 모양과 그림은 바이트 그대로, 본문 짜임 같음, 빠진 글자 0). 남은 1개는 한 줄에 날짜 칸과 쌍점 칸이 겹친 서식의 결함(고칠 것) | [repro/form-fill](repro/form-fill) — 서식 709개의 원 출처 주소·SHA-1 목록. 두 번 돌려 만든 파일 지문이 모두 같음 |
| 개인정보 찾기 — 공개 시험 [korean-pii-benchmark-v3](https://huggingface.co/datasets/schift-io/korean-pii-benchmark-v3) 473줄(정답은 그 시험의 표시, 채점 정의는 우리가 적음) | 사람 이름 찾음률 **95.6%**(정밀도 100%) · 주소 **97.9%**(100%) · 가리면 안 되는 문장 59줄 중 가린 줄 0. 약한 곳: 지역번호로 시작하는 일반 전화 43.1%(휴대전화는 모두 찾음). 이 시험은 규칙을 고칠 때 본 것이라 실제보다 높게 나올 수 있음 | [repro/korean-pii](repro/korean-pii) — `on-munseo-local@0.2.1`(서버 판과 같은 모델·같은 값). 다섯 번 돌려 473줄 찾은 자리가 모두 같음 |

- 이 판은 글자 인식이 없어 영어 PDF 값은 「글자 인식 없이」 값입니다. 서버 판(원격 On 문서)의 0.971·0.970 은 서버의 글자 인식 모델을 써서 이 대본으로는 재현되지 않습니다.
- 바탕 읽기 규칙은 이 벤치 200개를 보며 다듬었습니다. 그 밖의 숫자는 대본을 공개하지 않은 자체 측정이고, 정의는 [측정 자료](https://github.com/on-munseo/on-munseo.github.io/blob/main/docs/benchmark.md)에 있습니다.

**서버 판과 같은 결과.** 같은 커밋의 코드로 만들고, 같은 입력을 두 쪽에 보내 결과를 바이트까지 견줍니다(아래 [원격 On 문서와 같은 결과](#원격-on-문서와-같은-결과)).

**꾸러미 확인.** 도구별 한 줄은 판을 고정해 붙입니다(`on-munseo-local@0.2.1` — `setup` 이 판 번호를 적는 것은 0.2.1 다음 판부터, 0.2.1 까지의 `setup` 은 `@latest` 를 적음). npm 에 새 판이 올라와도 이미 붙인 판은 바뀌지 않고, 사람이 [올릴 때](#새-판으로-올리기)만 바뀝니다. 판마다 지문(SHA-256)은 [릴리스](https://github.com/on-munseo/on-local/releases)·[본 저장소 SHA256SUMS](https://github.com/on-munseo/on-munseo.github.io/blob/main/SHA256SUMS)에, 바뀐 점은 [CHANGELOG](CHANGELOG.md)에 있습니다.

**보안.** 우리 코드의 네트워크 부르기 0(`MANIFEST.json` 의 `netScan`) · Node 25 이상에서 네트워크·다른 프로그램 실행·네이티브 부품을 막고 띄움(`on_local_info`). 서비스 전체의 자체 보안 점검 요약(2026-11-21 전수 점검 — 높음 16건 모두 고침)은 [본 저장소 README](https://github.com/on-munseo/on-munseo.github.io#믿을-근거--남이-다시-확인할-수-있는-것)에 있습니다. 보안 문제는 공개 이슈 대신 [SECURITY.md](SECURITY.md)의 길로 알려 주세요 — 근무일 3일 안에 받았다고 답하고, 7일 안에 판단과 고칠 일정을 알립니다.

## 연결하기

두 줄 한 벌로 붙입니다. **첫 줄은 내 PC 판**(`on-local` — 읽기·만들기·점검·가리기, 이 컴퓨터 안에서만), **둘째 줄은 원격 법령 묶음**(`on-geungeo` — On 근거: 법령 원문·글 속 인용 확인)입니다. 법령 묶음에는 문서가 아니라 질문(법령 이름·조문 번호·인용을 확인할 글)만 갑니다. 둘째 줄을 빼고 첫 줄만 붙여도 됩니다.

**한 번에(setup)** — 이 PC 에 깔린 AI 도구를 찾아 설정 파일에 더합니다:

```bash
npx -y on-munseo-local@0.2.1 setup            # 첫 줄(내 PC 판)만 — 터미널에서 돌리면 둘째 줄을 붙일지 묻습니다
npx -y on-munseo-local@0.2.1 setup --pair     # 둘째 줄(법령 on-geungeo)까지
npx -y on-munseo-local@0.2.1 setup --dry-run  # 바꿀 것만 보기
npx -y on-munseo-local@0.2.1 setup --undo     # 이 명령이 더한 줄만 빼기
npx -y on-munseo-local@latest setup --update  # 새 판으로 올리기 — 등록된 줄의 판 번호만 바꿈(아래)
```

- 찾는 도구: Claude Code(`~/.claude.json` — `claude` 명령이 있으면 그 명령으로)·Claude 데스크톱·Codex(`~/.codex/config.toml`)·Cursor(`~/.cursor/mcp.json`)·VS Code(사용자 `mcp.json`).
- 설정 파일을 바꾸기 전에 그 옆에 백업(`<파일>.bak-<날짜시각>`)을 두고, 같은 이름이 이미 있으면 건너뜁니다(덮어쓰지 않음). 바꾼 뒤 다시 읽어 우리 줄이 맞고 다른 내용이 그대로인지 보고, 아니면 백업으로 되돌립니다.
- 더한 줄은 `~/.on-munseo-local/setup.json` 에 적어 두고, `--undo` 는 그 기록과 값이 그대로인 줄만 뺍니다(사람이 더했거나 고친 줄은 그대로). 전역 설치(폐쇄망 묶음 포함)로 돌리면 설정에 `npx` 대신 깔린 명령 `on-munseo-local` 을 적어 인터넷 없이 뜹니다.
- 주석이 든 설정·깨진 설정·낯선 꼴(예: Codex 의 `mcp_servers = { … }` 한 줄 표)·읽기 전용 설정은 건드리지 않고 손으로 더할 한 줄을 알려 줍니다. 심볼릭 링크 설정은 링크를 그대로 두고 가리키는 파일을 고칩니다.
- setup 도 네트워크를 쓰지 않습니다. 설정 파일만 읽고 쓰고, 법령 묶음은 주소를 글로만 적습니다. Claude 데스크톱의 법령 묶음은 설정 → 커넥터에서 주소로 붙입니다.

### 새 판으로 올리기

등록 줄에 판 번호를 적어 붙이므로(판 고정 — `on-munseo-local@0.2.1`) 새 판이 나와도 저절로 바뀌지 않습니다. npm 에 문제 있는 판이 올라와도 이미 붙인 판은 그대로입니다. [바뀐 점](CHANGELOG.md)을 보고 올릴 때만:

```bash
npx -y on-munseo-local@latest setup --update            # 등록된 on-local 줄의 판 번호만 새 판으로(바꾸기 전 백업)
npx -y on-munseo-local@latest setup --update --dry-run  # 바꿀 것만 보기
npx -y on-munseo-local@latest setup --update --to <옛 판>  # 옛 판으로 돌리기(새 판의 setup 이 옛 판 번호를 적음)
```

- 바꾸는 것은 등록 줄의 판 칸 하나뿐입니다. 다른 칸(환경 변수 등)과 다른 서버는 그대로이고, 등록되지 않은 도구에는 더하지 않습니다. setup 이 더한 줄이면 되돌리기 기록도 새 값으로 바꿔 `--undo` 가 계속 뺍니다.
- 전역 설치(`on-munseo-local` 명령)로 붙였으면 설정은 그대로 두고 `npm install -g on-munseo-local@<새 판>` 으로 올립니다.
- `setup --update` 가 없는 옛 판(0.2.1 까지)으로 붙였거나 그 판의 `setup` 으로 붙였으면(등록 줄이 `@latest`) 한 번만 손으로 판 번호를 바꿉니다 — Claude Code: `claude mcp remove -s user on-local` 뒤 `claude mcp add -s user on-local -- npx -y on-munseo-local@<새 판>`. 다른 도구는 설정 파일의 `on-munseo-local@…` 칸만 고칩니다.

도구마다 손으로 붙이려면:

**Claude Code** — 터미널에 붙여 넣습니다(`-s user` 는 모든 폴더에서 쓰기, 끝의 판 번호는 판 고정 — 자동으로 새 판을 받지 않음, 올리기는 [새 판으로 올리기](#새-판으로-올리기)):

```bash
claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1
claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
```

전역 설치 뒤에는 첫 줄을 이렇게 바꿉니다(띄울 때 npm 저장소에 묻지 않음):

```bash
npm install -g on-munseo-local
claude mcp add -s user on-local -- on-munseo-local
```

등록한 그 대화에는 도구가 아직 붙지 않습니다. 앱을 다시 켜거나 새 대화를 열면 그다음부터 씁니다. 열쇠가 없으면 법령 묶음은 로그인 단계를 건너뛰고 손님으로 씁니다.

**Codex(OpenAI)** — 설정 파일 `~/.codex/config.toml` 에 적습니다. 이렇게 붙이면 로그인 창이 뜨지 않고, 열쇠가 없으면 법령 묶음은 손님으로 씁니다:

```toml
[mcp_servers.on-local]
command = "npx"
args = ["-y", "on-munseo-local@0.2.1"]

[mcp_servers.on-geungeo]
url = "https://onmunseo.kr/mcp/law"
```

명령 줄 한 줄로는 `codex mcp add on-local -- npx -y on-munseo-local@0.2.1` 입니다. 원격 묶음을 `codex mcp add … --url` 로 붙이면 그때 곧바로 On 문서 로그인 창(브라우저)이 뜹니다 — 열쇠가 없으면 위 설정 파일 꼴을 씁니다. 읽기만 하는 도구에는 읽기 전용 표시(`readOnlyHint`)가 있어 Codex 가 승인을 묻지 않고 부릅니다. 파일을 새로 쓰는 `on_mask_hwpx` 에는 그 표시가 없습니다.

**Claude 데스크톱** — 맥 `~/Library/Application Support/Claude/claude_desktop_config.json` · 윈도우 `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "on-local": {
      "command": "npx",
      "args": ["-y", "on-munseo-local@0.2.1"]
    }
  }
}
```

저장한 뒤 Claude 데스크톱을 다시 켭니다. 법령 묶음(`https://onmunseo.kr/mcp/law`)은 설정 → 커넥터 → 「사용자 지정 커넥터 추가」에 주소를 넣어 붙입니다. 윈도우에서 `npx` 를 찾지 못하면 `"command": "cmd"`, `"args": ["/c", "npx", "-y", "on-munseo-local@0.2.1"]` 로 줍니다. 읽을 폴더·결과 폴더를 바꾸려면 `on-local` 에 `"env": { "ONDOC_LOCAL_READ": "D:\\문서", "ONDOC_LOCAL_OUT": "D:\\On문서_결과" }` 를 더합니다([설정](#설정)).

**Cursor** — `~/.cursor/mcp.json`(모든 프로젝트) 또는 프로젝트의 `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "on-local": {
      "command": "npx",
      "args": ["-y", "on-munseo-local@0.2.1"]
    },
    "on-geungeo": {
      "url": "https://onmunseo.kr/mcp/law"
    }
  }
}
```

**VS Code** — 사용자 설정 `mcp.json`(명령 팔레트 「MCP: Open User Configuration」) 또는 작업 공간의 `.vscode/mcp.json`:

```json
{
  "servers": {
    "on-local": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "on-munseo-local@0.2.1"]
    },
    "on-geungeo": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/law"
    }
  }
}
```

**폐쇄망(업무망)** — 인터넷이 되는 곳에서 받은 「부품까지 묶은 판」(`on-munseo-local-<판>-offline.tgz`)을 옮겨 `npm install -g --offline on-munseo-local-<판>-offline.tgz` 로 깝니다. 인터넷 없이 깔리고 돕니다. 원격 묶음은 닿지 않으므로 첫 줄(`on-local`)만 붙입니다(`on-munseo-local setup`).

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
| 만들기(0.2.0) — 공문서 쓰기 30과제(짜임·원고)·표 81·예시 양식 66종 채우기·다듬기 90, 공개 문서 153개의 HWPX 바꾸기·채울 곳 찾기·서식 채우기 | 30과제 + 153개 | 628번 | **628번**(만든 한글 419개 같음) |
| 운영 중인 원격 서버(`onmunseo.kr`, 손님)에 직접 — `on_read` | 6개(한글·옛 한글·PDF·워드·엑셀·파워포인트) | 6번 | 6번 |
| 맥(arm64, Node 25.9) ↔ 윈도우 11(x64, Node 26.13), 이 꾸러미끼리 | 153개 | 1,013번 | 1,013번 |
| 공개 문서 더 — 위 출처 + 부처 공개 문서(한글·PDF), 아이맥(Node 22) | 2,026개(한글 1,304·PDF 540·워드 61·엑셀 60·파워포인트 61) | 27,644번 | **27,644번** |

- 견준 도구: 글(가림 포함)·형식·문서 정보·표(마크다운·JSON)·조각·결재점검·개인정보 찾기·가린 글·가린 한글·대비표, 그리고 붙여 넣은 글(`text`)로 주는 길. 맞은 결과는 바이트까지 같습니다. 공개 문서 153개는 운영체제 네트워크 막기(macOS sandbox-exec)와 Node 권한 모델 안에서 돌렸습니다.
- 가린 한글 파일은 zip 압축 바이트가 기계(Node 판·CPU)에 따라 달라질 수 있습니다. 같은 기계에서는 원격 서버 꾸러미와 바이트까지 같았고(29개), 맥↔윈도우는 압축 바이트가 달라도 풀어 낸 내용(본문 XML 등)이 모두 같았습니다.
- 그림이 너무 큰 문서처럼 입구에서 거절하는 문서는 같은 까닭 글로 거절합니다.
- 만든 한글은 풀어서 칸마다 견줍니다. 문서 정보의 만든 시각(`CreatedDate`·`ModifiedDate`·`date`)은 만든 그때 시각이라 두 쪽을 몇 초 사이로 부르면 다를 수 있어 그 칸만 빼고 봤습니다(419개 가운데 20개가 그 칸만 다름, 나머지는 바이트까지 같음).
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
| `ONDOC_LOCAL_TOOLS` | 켤 도구 묶음만(쉼표로 — `text` 읽기·`check` 점검·`mask` 가리기·`hwpx` 한글 만들기·`gov` 공문서 쓰기·`tidy` 다듬기, 줄임 `read`·`write`(gov+hwpx)·`all`, 도구 이름도 됨). 제품별 플러그인을 여럿 깔아도 도구가 겹치지 않게 씁니다. `on_local_info` 는 늘 켭니다 | 모두 |

`ONDOC_LOCAL_READ` 로 좁혔을 때 그 밖 파일은 「허락 밖」이라고만 답합니다(있는지도 알려 주지 않음).

## 알아 둘 점

- **글자 인식(스캔 쪽·사진)은 없습니다.** 스캔한 PDF 쪽·그림 파일에서는 글이 나오지 않습니다. 필요하면 원격 On 문서(`https://onmunseo.kr/mcp/text`, `ocr: true` — 열쇠)를 따로 붙여 씁니다. 그때는 그 문서가 서버로 갑니다.
- **그래프·체계도 그림·쪽 그림·PDF 는 없습니다.** 그림 부품(네이티브)이 있어야 해서입니다. `on_write_gov` 원고의 그래프·체계도는 이 판에서 그림 대신 표로 들어갑니다. 그림이 필요하면 원격 On 문서(`https://onmunseo.kr/mcp`)를 따로 붙여 씁니다 — 그때는 원고가 서버로 갑니다.
- **법령(On 근거)은 원격입니다**(`https://onmunseo.kr/mcp/law`). 그 도구에 넣은 법령 이름·조문 번호·글(인용 확인)이 서버로 가며, 문서 원문을 넣지 않으면 문서는 가지 않습니다.
- **보안 등급 표시(대외비 등)가 있는 문서는 처리하지 않습니다.** 이 판도 결과를 AI 에게 넘기기 때문입니다.
- **한도는 원격 서버와 같습니다.** 문서 하나 25MB, 압축을 푼 크기·문단 하나의 글 조각 수·표 칸 수·그림 크기 한도도 같습니다. 분당 요청 한도·하루 몫은 없습니다(혼자 쓰는 컴퓨터).
- **결과는 참고용입니다.** 결재 전에 사람이 확인해 주세요. 가린 한글은 한 글자 묶음 안에 든 값만 가리므로 결과를 다시 확인하세요(`on_find_pii`).

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

**On Munseo — Local** (`on-munseo-local`) is an MCP server that runs entirely on your computer. It reads Hangul (HWP/HWPX/HML), PDF, Word, Excel and PowerPoint files, writes Korean government-style HWPX documents (reports, plans, result reports, press releases), fills 66 example templates and HWP forms, converts documents to HWPX, checks official-document style and masks personal information — rule-based, without any language model.

- **Your documents stay on your machine.** It talks to your AI app over stdio only and uses no network: no update checks, no telemetry. Our code imports no network modules (checked at build time, see `netScan` in `MANIFEST.json`). On Node 25+, it relaunches itself under the Node permission model with network, child processes and native add-ons denied, file writes limited to the output folder. Ask your AI to call `on_local_info` to verify (`blocked_by_node: true`, `network_modules_loaded: []`).
- **Same results as the remote server.** Built from the same commit as the remote On Munseo MCP (`https://onmunseo.kr/mcp`). On 2026-11-26, 153 public documents gave identical results in all 2,091 tool calls; the document-writing tools (government-style reports, 66 templates, tables, forms, HWPX conversion, rewriting) matched in all 628 calls; a larger run over 2,026 public documents matched in all 27,644 calls; 6 calls against the live server matched byte for byte; macOS and Windows 11 builds matched in all 1,013 calls (masked HWPX files: same contents, zip bytes may differ by platform).
- **Install:** register it with your AI tool — `npm install -g` alone does not connect it. Claude Code: `claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1`. Codex: `codex mcp add on-local -- npx -y on-munseo-local@0.2.1`. Claude Desktop / Cursor: `"command": "npx", "args": ["-y", "on-munseo-local@0.2.1"]`. Or run `npx -y on-munseo-local@0.2.1 setup` to find the AI tools installed on this computer and add it to each (backs up each config first, skips existing entries, `--dry-run`, `--undo`; no network). For Korean statute texts and citation checks, also add the remote law bundle `https://onmunseo.kr/mcp/law` (`setup --pair`) — only your questions, not your documents, are sent to it.
- **Pinned version:** registration lines pin the version (`on-munseo-local@0.2.1`); nothing updates by itself. To update: `npx -y on-munseo-local@latest setup --update` (changes only the version in registered entries, backs up first, `--dry-run`). Changes: [CHANGELOG](CHANGELOG.md).
- **Re-runnable numbers:** opendataloader-bench (200 English PDFs, official scorer unchanged) overall 0.945 with this npm package alone (no OCR) — [script](repro/opendataloader-bench); form filling on 709 public statute forms: 653 of the 654 filled files keep the original form byte-for-byte outside the filled text — [script](repro/form-fill). Security reports: [SECURITY.md](SECURITY.md).
- **What goes to your AI:** text returned by a tool enters your AI conversation (and the AI provider, if it is a cloud service). To keep originals out of the chat, use `on_mask_hwpx` (writes the masked file only), `on_find_pii` (kinds and counts) or `mask: true`.
- **Not included:** OCR for scanned pages, chart and diagram images, page images and PDF output (they need a native graphics library) — use the remote server for those (documents are then sent to it). Charts and diagrams in a drafted document become tables. Documents with security classification marks are refused. Results are for reference; please review before use.
- **Terms:** free to use for individuals and organizations, including at work; no reverse engineering, no redistribution of modified versions, no resale — see `LICENSE.md`. Open-source components keep their own licenses (`NOTICE.md`).
