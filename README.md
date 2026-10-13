# card-assets — 앱인토스 미니앱 카드 이미지 에셋

앱 번들에 넣기엔 큰 **완성 카드 이미지**를 두는 공개 저장소. 앱은 jsDelivr 의 **태그 URL**로 받는다(CORS `*` — fetch → base64 저장이 된다).

```
https://cdn.jsdelivr.net/gh/app-in-hungry/card-assets@<태그>/<앱>/<특집>/<id>.jpg
```

| 앱 | 특집 | 태그 | 내용 |
|---|---|---|---|
| `morning-card/` (아침 인사 카드 · app34) | `chuseok-2026/` | `chuseok-2026-v1` | 추석 2026 카드 50장 · 1080×1440 JPEG · 글자가 그림 안에 있다 · `manifest.json`(id · 단계 · 글 줄) |
| `morning-card/` | `scenes/` | **`scenes-v4`**(가을 + 겨울 + 봄 + 여름 124장면 · v3 = 가을 + 겨울 · v1 = 가을만 · v2 는 쓰지 않음 — 아래 규칙) | 장면 바탕 그림 — 계절마다 31장면 × 2(기본 · 좌우 뒤집음) · 1080×1440 JPEG · 글자 없음(앱이 날짜 · 카드 판 · 해님이를 얹는다) · `manifest.json`(id · 계절 · 주인공 · 팔레트 · 말풍선 자리). 만드는 곳 `app34-morning-card/tools/shorts/stills.mjs`(유튜브 쇼츠와 같은 장면) · 계절이 늘면 누적 태그 `scenes-v2` … |
| `morning-card/` | `shorts/` | 릴리스 `shorts-rN` | 유튜브 쇼츠 영상(30초 · 1080×1920 · 날마다 한 편)은 **저장소가 아니라 깃허브 릴리스 파일**(`releases/download/shorts-rN/YYYY-MM-DD.mp4`) · 목록 `shorts/manifest.json` 만 저장소에(IFTTT 가 **raw 주소**로 매일 06:00 읽는다). 만드는 곳 `app34-morning-card/tools/shorts/`(batch · publish · IFTTT.md) |

## 규칙

- **저장소 트리는 50MB 아래로**: jsDelivr 는 태그 시점 트리가 50MB 를 넘으면 그 태그의 파일을 거절한다("Package size exceeded the configured limit of 50 MB" · 2026-10-13 shorts 영상 341MB 를 트리에 넣었다가 scenes-v2 가 깨짐). 큰 파일(영상)은 릴리스 파일로.

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
