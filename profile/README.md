<h1 align="center">slopdam</h1>

<p align="center">
  A dam for AI slop: em dashes, emoji, separator lines and markdown stay out of your logs.<br>
  로그로 흘러드는 AI slop을 막는 댐: 긴 대시, 이모지, 구분선, 마크다운이 로그에 남지 않게 합니다.
</p>

<p align="center">
  <a href="https://github.com/slopdam/slopdam"><img alt="Repository" src="https://img.shields.io/badge/repo-slopdam-5A9BF0?logo=github"></a>
  <a href="https://pypi.org/project/slopdam/"><img alt="PyPI" src="https://img.shields.io/pypi/v/slopdam?label=PyPI&color=7ED6A7"></a>
  <a href="https://www.npmjs.com/package/@slopdam/core"><img alt="npm" src="https://img.shields.io/npm/v/@slopdam/core?label=npm&color=7ED6A7"></a>
  <a href="https://github.com/slopdam/slopdam/blob/main/LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-FFC857"></a>
  <img alt="English and Korean" src="https://img.shields.io/badge/lang-EN%20%7C%20KO-F48FB1">
</p>

---

<p align="center">
  <img src="https://raw.githubusercontent.com/slopdam/slopdam/main/docs/assets/demo.gif" alt="slopdam demo: a Python app logging reader text to the console and dev text to a file, slopdam check finding traces in Python and JavaScript log calls, slopdam fix previewing a diff, and slopdam clean in a pipe" width="860">
</p>

AI coding tools leave the same traces in log messages: `—` and `ㅡ` dashes, ✅🚀 emoji, `=====` separators, `**bold**`, curly quotes. slopdam removes them while logs are written, and finds and fixes them in source code before a commit. It uses deterministic rules, not a model, so the same input always gives the same output.

AI 코딩 도구는 로그 메시지에 늘 같은 흔적을 남깁니다. slopdam은 로그가 출력될 때 이를 정리하고, 커밋 전에 소스 코드에서 찾아 고칩니다. 모델이 아니라 결정적 규칙으로 동작하므로 같은 입력에는 언제나 같은 결과가 나옵니다.

```
input : ✅ **저장 완료** ㅡ 2024–2025년 데이터 3건 처리했습니다! 🎉
reader: 저장 완료: 2024~2025년 데이터 3건 처리했습니다.
dev   : [OK] 저장 완료 - 2024-2025년 데이터 3건 처리했습니다!
```

`reader` is plain text for people; `dev` keeps information for tools, turning status emoji into `[OK]`, `[FAIL]` and `[WARN]`. · `reader`는 사람이 읽는 글, `dev`는 도구가 쓰는 글입니다.

## Packages · 패키지

| Language | Install | Clean logs as they are written | Find and fix in source code |
|---|---|---|---|
| Python | `pip install slopdam` | `logging` formatter and filter, structlog, loguru | `slopdam check`, `slopdam fix`, pre-commit, GitHub Action |
| JavaScript, TypeScript | `npm install @slopdam/core` | pino, winston | ESLint rule `slopdam/no-slop` with autofix |
| Any language | `pip install slopdam` | `your-app \| slopdam clean` | `slopdam check` for JS, TS, Java, Kotlin, Go, Rust, Ruby, PHP, Swift |

Both packages are tested against one language-neutral [spec](https://github.com/slopdam/slopdam/blob/main/spec/README.md) on every pull request, so they give the same output. · 두 패키지는 PR마다 같은 언어 중립 명세로 테스트하므로 결과가 같습니다.

## Why slopdam · 이런 점이 좋습니다

- Korean-aware: the Hangul `ㅡ` in all three code points, `!` after Hangul, and `~` for number ranges. · 한국어를 압니다: 한글 `ㅡ`, 한글 뒤 `!`, 숫자 범위 `~`.
- Conservative: URLs, inline code, `key=value` values, file paths, dates and flags are never changed, and cleaning twice changes nothing. · 보수적: URL, 코드, 경로, 날짜, 옵션은 건드리지 않고, 두 번 정리해도 같습니다.
- Safe fixes: only the text inside string literals changes; quotes, escapes, `%s` and `${...}` stay. · 안전한 수정: 문자열 안의 글자만 고칩니다.
- Fits CI: pull request annotations, SARIF for code scanning, JSON, stdin. · CI에 바로: PR 주석, SARIF, JSON, 표준 입력.
- No runtime dependencies, in either language. · 두 언어 모두 실행 의존성이 없습니다.

## A quick look · 미리보기

<table>
  <tr>
    <td align="center"><img src="https://raw.githubusercontent.com/slopdam/slopdam/main/docs/assets/logging-en.png" alt="python app.py prints reader text, and app.log holds the dev text with an [OK] tag" width="420"><br><sub>Clean log output · 로그 출력 정리</sub></td>
    <td align="center"><img src="https://raw.githubusercontent.com/slopdam/slopdam/main/docs/assets/check-ko.png" alt="slopdam check lists each trace with file, line, column, rule ID and fix" width="420"><br><sub>Find traces in Python and JavaScript · 흔적 찾기</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="https://raw.githubusercontent.com/slopdam/slopdam/main/docs/assets/fix-en.png" alt="slopdam fix --diff keeps the %d placeholders" width="420"><br><sub>Fix Python string literals · 문자열 수정</sub></td>
    <td align="center"><img src="https://raw.githubusercontent.com/slopdam/slopdam/main/docs/assets/pipe-ko.png" alt="slopdam clean in a pipe, reader and dev" width="420"><br><sub>Any program's output in a pipe · 파이프로 정리</sub></td>
  </tr>
</table>

## Try it · 써보기

```bash
pip install slopdam
echo '✅ **Deployed** v2 — all checks passed! 🚀' | slopdam clean      # Deployed v2: all checks passed!
slopdam check src/
```

```js
// eslint.config.js
import slopdam from "@slopdam/core/eslint";
export default [slopdam.configs.recommended];
```

Guides: [Python](https://github.com/slopdam/slopdam#readme) · [JavaScript](https://github.com/slopdam/slopdam/blob/main/js/README.md) · 한국어: [Python](https://github.com/slopdam/slopdam/blob/main/README.ko.md) · [JavaScript](https://github.com/slopdam/slopdam/blob/main/js/README.ko.md)

## Roadmap · 로드맵

Released: Python core, CLI and integrations (0.4), JavaScript and TypeScript with pino, winston and ESLint (0.5). Next: Go and the JVM, then Rust and editor support. See the [roadmap](https://github.com/slopdam/slopdam/blob/main/ROADMAP.md) · [로드맵](https://github.com/slopdam/slopdam/blob/main/ROADMAP.ko.md).

## Get involved · 참여하기

- Bugs, missed traces, wrong changes: [Issues](https://github.com/slopdam/slopdam/issues) · 버그와 놓친 흔적은 이슈로
- Questions and ideas: [Discussions](https://github.com/slopdam/slopdam/discussions) · 질문과 아이디어는 토론으로
- Contributing: [CONTRIBUTING](https://github.com/slopdam/slopdam/blob/main/CONTRIBUTING.md) (DCO sign-off) · 기여 안내

<p align="center"><sub>Open source under the MIT License</sub></p>
