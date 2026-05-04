# FLOW ZoomIt for Mac (한국어)

> 한국어 강의·워크숍·코칭을 위한 [ZoomacIt](https://github.com/07JP27/ZoomacIt)(Swift 6 + AppKit 네이티브 macOS 메뉴바 앱) 기반의 macOS 호환판. 손글씨 폰트·FLOW 펜 기본값·양국어 UX 포함. Windows 의 [FLOW ZoomIt](https://github.com/Demian-Yim/flow-zoomit) 의 Mac 짝꿍.

🇬🇧 [English README →](README.md)
🇯🇵 일본어 (원본): [README_ja.md](README_ja.md)

---

## 왜 만들었나

[FLOW ZoomIt for Windows](https://github.com/Demian-Yim/flow-zoomit) 는 Microsoft Sysinternals ZoomIt v11.0 에 한국어 손글씨 폰트와 6색 펜 팔레트를 입혀 배포 중입니다. 그러나 **Microsoft 가 ZoomIt 을 macOS 로 포트하지 않았기 때문에** Mac 사용자는 사용할 수 없었습니다.

다행히 [@07JP27](https://github.com/07JP27) 이 만든 오픈소스 [**ZoomacIt**](https://github.com/07JP27/ZoomacIt) (Swift 6 + AppKit 네이티브) 이 ZoomIt 의 정신적 클론으로 활발히 개발 중입니다. 이를 GPL-3.0 라이선스 하에 포크해 한국어 강의 디폴트(손글씨 폰트·6색 펜·B/W 안전 가이드)를 입혀 **FLOW ZoomIt for Mac** 을 만들었습니다.

---

## ⚠️ 현재 상태: v0.1 — 초기 포크

이건 **첫 빌드**입니다. 공개 배포 전 다음을 검증해야 합니다:

| 항목 | 검증 방법 | 책임 |
|---|---|---|
| 1. 한글 IME 입력 | Mac 에서 빌드 후 ⌃2 → T → 한/영 → 한글 입력 | Day 1 핵심 가설 |
| 2. 손글씨 폰트 fallback | Settings UI 에서 폰트 변경 → 그리기 | 사용자 검증 |
| 3. macOS 26+ 호환 | macOS Tahoe (26.0) 에서 정상 실행 | 자가 검증 |
| 4. 6색 펜 전환 | 그리기 모드에서 R/G/B/Y/O/P 전환 | 자가 검증 |

자세한 빌드·검증 가이드: [docs/MAC_BUILD_HANDOFF.md](docs/MAC_BUILD_HANDOFF.md)

---

## 단축키

| 키 | 동작 |
|---|---|
| `⌃1` | 정적 줌 |
| `⌃2` | 그리기 모드 |
| `⌃3` | 휴식 타이머 |

### 그리기 모드 단축키

| 키 | 동작 |
|---|---|
| `R G B Y O P` | 펜 색상: 빨강·초록·파랑·노랑·주황·핑크 |
| `Drag` | 자유 펜 |
| `Shift+Drag` | 화살표 |
| `Control+Drag` | 사각형 |
| `Tab+Drag` | 타원 |
| `Shift+Control+Drag` | 직선 |
| `Wheel` | 펜 굵기 조절 |
| `T` | 텍스트 모드 |
| **`B`** | ⚠️ 검정 캔버스 덮어쓰기 — `⌘Z` 로 취소 |
| **`W`** | ⚠️ 흰 캔버스 덮어쓰기 — `⌘Z` 로 취소 |
| `E` | 모든 그림 지우기 |
| `⌘Z` | 되돌리기 (B/W 덮어쓰기 취소 포함) |
| `Esc` | 그리기 종료 |

---

## ⚠️ `B`/`W` 캔버스 덮어쓰기 주의 (Windows 와 동일)

그리기 모드(⌃2)에서 **`T` 를 누르기 전**에 한/영을 한국어로 바꾸고 자모를 입력하면, 첫 키가 `b`(=ㅠ) 또는 `w`(=ㅈ) 일 때 화면이 통째로 검정·흰색으로 덮입니다 — 이는 ZoomacIt 의 단독 단축키 동작입니다. 두벌식에서 ㅈ(자/저/주/지)·ㅠ가 흔하기 때문에 강의 중 사고가 잦습니다.

✅ **안전 순서:** `⌃2` → **`T` 먼저** → 캔버스 클릭 → `한/영` → 한글 입력
🆘 **사고 시 복구:** `⌘Z` 한 번 — 캔버스 덮어쓰기 즉시 취소

(자세한 배경: Windows v1.0.1 릴리스 노트 — <https://github.com/Demian-Yim/flow-zoomit/releases/tag/v1.0.1>)

---

## FLOW 디폴트

| 설정 | 값 |
|---|---|
| 본체 / Engine | ZoomacIt v0.5+ (07JP27) Swift 6 / AppKit |
| Bundle ID | `kr.flowdesign.ZoomacIt` |
| 표시 이름 | `FLOW ZoomIt` |
| 기본 폰트 가중치 | **Bold** (손글씨 강조 톤) |
| 기본 폰트 패밀리 | 시스템 기본 → fallback: `Apple SD Gothic Neo Bold` (한국어 친화) |
| 펜 색상 6색 | Red·Green·Blue·Yellow·Orange·Pink (R/G/B/Y/O/P) |
| 펜 색상 기본 | Red |
| 휴식 타이머 기본 | 600초 (10분) |
| 줌 배율 기본 | 2.0× |

설정 변경: 메뉴바 아이콘 → Settings...

---

## 라이선스

**GPL-3.0** — 업스트림 [ZoomacIt](https://github.com/07JP27/ZoomacIt) 에서 상속. 소스 코드 GitHub 에 공개. 라이선스 변경 불가.

### 크레딧

- **원작 / Upstream:** [ZoomacIt by 07JP27](https://github.com/07JP27/ZoomacIt) — 모든 핵심 엔지니어링 크레딧은 여기로
- **FLOW 포크:** [FLOW: AX 디자인연구소](https://flowdesign.ai.kr) by **임정훈 소장**, AI 코디네이터. 한국어 강의 디폴트, 양국어 UX, FLOW 브랜딩
- **영감:** Microsoft Sysinternals ZoomIt for Windows — 20여 년간 강의·발표 도구의 표준

---

## 관련 프로젝트

- **Windows 버전**: <https://github.com/Demian-Yim/flow-zoomit> — Sysinternals ZoomIt v11.0 + FLOW 한국어 디폴트
- **라이브 데모**: <https://flowdesign.ai.kr>

---

© 2026 FLOW: AX 디자인연구소 — 포크 콘텐츠. 업스트림 코드 © 2025–2026 07JP27 (GPL-3.0).
