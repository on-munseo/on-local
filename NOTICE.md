# 사용 구성요소 고지

본 제품은 한글과컴퓨터의 한글 문서 파일(.hwp) 공개 문서를 참고하여 개발하였습니다.

On 문서 내 PC 판에 든 오픈소스 부품입니다. 엔진·코드는 on-munseo 의 것이며 무단 복제·배포·재사용·역공학을 허락하지 않습니다(이용약관 제5조). 오픈소스 부품은 각 라이선스를 따르며, 이 고지가 그 라이선스가 주는 권리를 줄이지 않습니다.

| 부품 | 쓰는 곳 | 라이선스 — 전문 |
|---|---|---|
| rhwp (Copyright (c) 2025-2026 Edward Kim) | 한글 엔진(server/rhwp)의 바탕 | MIT — licenses/rhwp-MIT.txt |
| 이음오피스 고침 (github.com/pblsketch, Copyright 2026 Mainfunc, Inc.) | 한글 엔진에 옮겨 쓴 고침 2개 — 우리 엔진에 맞게 고쳐 씀 | Apache-2.0 — licenses/IeumOffice-Apache-2.0.txt |
| pdf.js (Mozilla) | PDF 글 위치 읽기(node_modules/pdfjs-dist — 쓰는 파일만 담음) | Apache-2.0 — node_modules/pdfjs-dist/LICENSE |
| MCP TypeScript SDK (Anthropic) · Zod · JSZip | AI 도구 연결 · 입력 확인 · 한글(HWPX) 묶음 | MIT(JSZip 은 MIT·GPL-3.0 가운데 MIT) — 설치되는 각 부품 폴더의 LICENSE |
| CanvasKit (Skia, Google — canvaskit-wasm 0.42.0) | 쪽 그림을 그리는 그림 부품(local/canvaskit — wasm, 네이티브 부품 아님. 시범판 편집 화면이 쓰는 것과 같은 파일) | BSD-3-Clause, Copyright (c) 2011 Google Inc. — licenses/canvaskit-BSD-3-Clause.txt. wasm 안의 제3자 부품은 아래 표 |
| On폭 글꼴(OnPok — Noto Sans KR·Noto Serif KR 바탕, 백묵 바탕 6종 포함) | 쪽 그림의 글꼴(local/fonts — 본 파일 24개 + 한자·드문 한글 대표) | SIL OFL 1.1 — licenses/OnFonts-OFL.txt · 백묵 글꼴 고지 licenses/OnFonts-Baekmuk-COPYRIGHT.txt |

### CanvasKit wasm 안의 제3자 부품

canvaskit-wasm 0.42.0 을 만든 Skia 커밋(e2def78f, 2026-08-18)의 DEPS 에 적힌 판입니다. 라이선스 원문은 그 판의 공식 저장소에서 그대로 옮겨 licenses/canvaskit/ 에 두었고, 판·출처·지문은 licenses/canvaskit/README.md 에 있습니다.

| 부품 | 판 | 라이선스 — 원문 |
|---|---|---|
| FreeType | 2.14.2 | FreeType License(FTL) — licenses/canvaskit/freetype-LICENSE.TXT · freetype-FTL.TXT |
| HarfBuzz | 13.1.0 | Old MIT — licenses/canvaskit/harfbuzz-COPYING |
| ICU | 78.2 | Unicode License v3 외(같은 파일) — licenses/canvaskit/icu-LICENSE |
| libpng | 1.6.56 | PNG Reference Library License v2 — licenses/canvaskit/libpng-LICENSE |
| zlib(Chromium) | 1.3.0.1 | zlib License — licenses/canvaskit/zlib-LICENSE |
| libjpeg-turbo | 3.1.0 | IJG License · Modified BSD · zlib License — licenses/canvaskit/libjpeg-turbo-LICENSE.md · libjpeg-turbo-README.ijg |
| libwebp | 1.4.0 | BSD-3-Clause + Additional IP Rights Grant — licenses/canvaskit/libwebp-COPYING · libwebp-PATENTS |
| Wuffs | 0.3.3 | Apache-2.0 — licenses/canvaskit/wuffs-LICENSE |
| Brotli | 1.0.9 | MIT — licenses/canvaskit/brotli-LICENSE |
| Emscripten 실행부(겉 JS·musl libc·libc++·libc++abi·compiler-rt) | 4.0.7 | MIT 또는 NCSA · MIT · Apache-2.0 WITH LLVM-exception — licenses/canvaskit/emscripten-LICENSE · emscripten-musl-COPYRIGHT · emscripten-libcxx-LICENSE.TXT · emscripten-libcxxabi-LICENSE.TXT · emscripten-compiler-rt-LICENSE.TXT |

- Portions of this software are copyright © 2026 The FreeType Project (https://freetype.org). All rights reserved.
- This software is based in part on the work of the Independent JPEG Group.

개인정보 찾기 모델(server/models/pii_v*)은 On 문서 팀이 처음부터 학습한 것입니다(남이 학습한 바탕 모델 없음).

## 상표

「한글」·「한컴」·「HWP」·「HWPX」는 주식회사 한글과컴퓨터의 상표(등록상표 포함)입니다. 이 프로그램은 한글과컴퓨터와 제휴·후원·승인 관계가 없는 독립 프로그램입니다. HWPX 는 한국산업표준 KS X 6101(OWPML)을 따르는 문서 형식입니다.

"Hangul", "Hancom", "HWP", and "HWPX" are trademarks or registered trademarks of Hancom Inc. This program is independent and has no affiliation, sponsorship, or endorsement by Hancom Inc.
