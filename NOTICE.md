# 사용 구성요소 고지

본 제품은 한글과컴퓨터의 한글 문서 파일(.hwp) 공개 문서를 참고하여 개발하였습니다.

On 문서 내 PC 판에 든 오픈소스 부품입니다. 엔진·코드는 on-munseo 의 것이며 무단 복제·배포·재사용·역공학을 허락하지 않습니다(이용약관 제5조). 오픈소스 부품은 각 라이선스를 따르며, 이 고지가 그 라이선스가 주는 권리를 줄이지 않습니다.

| 부품 | 쓰는 곳 | 라이선스 — 전문 |
|---|---|---|
| rhwp (Copyright (c) 2025-2026 Edward Kim) | 한글 엔진(server/rhwp)의 바탕 | MIT — licenses/rhwp-MIT.txt |
| 이음오피스 고침 (github.com/pblsketch, Copyright 2026 Mainfunc, Inc.) | 한글 엔진에 옮겨 쓴 고침 2개 — 우리 엔진에 맞게 고쳐 씀 | Apache-2.0 — licenses/IeumOffice-Apache-2.0.txt |
| pdf.js (Mozilla) | PDF 글 위치 읽기(node_modules/pdfjs-dist — 쓰는 파일만 담음) | Apache-2.0 — node_modules/pdfjs-dist/LICENSE |
| MCP TypeScript SDK (Anthropic) · Zod · JSZip | AI 도구 연결 · 입력 확인 · 한글(HWPX) 묶음 | MIT(JSZip 은 MIT·GPL-3.0 가운데 MIT) — 설치되는 각 부품 폴더의 LICENSE |

개인정보 찾기 모델(server/models/pii_v*)은 On 문서 팀이 처음부터 학습한 것입니다(남이 학습한 바탕 모델 없음).

## 상표

「한글」·「한컴」·「HWP」·「HWPX」는 주식회사 한글과컴퓨터의 상표(등록상표 포함)입니다. 이 프로그램은 한글과컴퓨터와 제휴·후원·승인 관계가 없는 독립 프로그램입니다. HWPX 는 한국산업표준 KS X 6101(OWPML)을 따르는 문서 형식입니다.

"Hangul", "Hancom", "HWP", and "HWPX" are trademarks or registered trademarks of Hancom Inc. This program is independent and has no affiliation, sponsorship, or endorsement by Hancom Inc.
