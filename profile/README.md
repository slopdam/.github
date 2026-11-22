## slopdam

A dam for AI slop, before it floods your logs and screens.

Code and text written with AI leave traces: `—` and `ㅡ` dashes, ✅🚀 emoji, `=====` separators, `**bold**`. slopdam filters them at output time (a logger formatter) and at commit time (a linter).

```
input : ✅ **Saved** — processed 3 rows for 2024–2025! 🎉
reader: Saved: processed 3 rows for 2024~2025!
dev   : [OK] Saved - processed 3 rows for 2024-2025!
```

| Repository | Description |
|---|---|
| [slopdam](https://github.com/slopdam/slopdam) | Open source core (MIT): Python logger formatter, linter and CLI |

```bash
pip install slopdam
```

### 한국어

AI가 만든 코드와 글에 남는 대시, 이모지, 구분선, 마크다운 흔적을 출력 단계와 커밋 단계에서 걸러냅니다. 한글 `ㅡ` 대시와 한국어 문장 부호도 처리합니다.

```
입력  : ✅ **저장 완료** ㅡ 2024–2025년 데이터 3건 처리했습니다! 🎉
reader: 저장 완료: 2024~2025년 데이터 3건 처리했습니다.
dev   : [OK] 저장 완료 - 2024-2025년 데이터 3건 처리했습니다!
```

문서: [README (한국어)](https://github.com/slopdam/slopdam/blob/main/README.ko.md)
