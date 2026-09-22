# card-assets — 앱인토스 미니앱 카드 이미지 에셋

앱 번들에 넣기엔 큰 **완성 카드 이미지**를 두는 공개 저장소. 앱은 jsDelivr 의 **태그 URL**로 받는다(CORS `*` — fetch → base64 저장이 된다).

```
https://cdn.jsdelivr.net/gh/app-in-hungry/card-assets@<태그>/<앱>/<특집>/<id>.jpg
```

| 앱 | 특집 | 태그 | 내용 |
|---|---|---|---|
| `morning-card/` (아침 인사 카드 · app34) | `chuseok-2026/` | `chuseok-2026-v1` | 추석 2026 카드 50장 · 1080×1440 JPEG · 글자가 그림 안에 있다 · `manifest.json`(id · 단계 · 글 줄) |

## 규칙

- **태그 URL 만 쓴다**(`@main` 금지). jsDelivr 는 태그 URL 을 영구 캐시한다 — 그림을 바꾸면 파일을 덮어쓰지 말고 **새 태그**(`…-v2`)를 붙이고 앱의 매니페스트(`SPECIAL.tag`)를 올린다.
- 파일 이름은 `{id}.jpg`(두 자리) — 앱의 저장 기록 키 · 매니페스트 id 와 같다. id 는 바꾸지 않는다.
- 생성 · 검증 · 규격화 도구와 **글 원문의 정본**은 각 앱 저장소(`app34-morning-card/tools/gen-cards/`)에 있다. 여기엔 결과물만.
- 그림은 제미나이 이미지 API 생성물(사람 · 실존 인물 · 워터마크 없음). 레퍼런스(남의 카드)는 절대 올리지 않는다.

## 올리는 순서 (맥)

```bash
cd /Users/fulltimescam/fulltimescam/appintoss/app34-morning-card/tools/gen-cards
npm install && node build.mjs          # → ../../../CARD-ASSETS/morning-card/chuseok-2026/{01..50}.jpg + manifest.json
cd /Users/fulltimescam/fulltimescam/appintoss/CARD-ASSETS
git add . && git commit -m "morning-card 추석 2026 chuseok-2026-v1" && git tag chuseok-2026-v1 && git push && git push --tags
```

확인: 폰 브라우저에서 `https://cdn.jsdelivr.net/gh/app-in-hungry/card-assets@chuseok-2026-v1/morning-card/chuseok-2026/01.jpg`
