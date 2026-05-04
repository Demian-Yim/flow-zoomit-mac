# FLOW ZoomIt for Mac — Build & Day 1 Validation Guide

> **For:** 데미안 님 (with MacBook), reading this when ready to build & test on macOS.
> **Status:** v0.1 first build — code changes done, build/sign/test outstanding.

---

## TL;DR (5 단계)

1. **Mac 에서 저장소 클론**
2. **Apple Developer Team ID 환경변수 설정**
3. **`make generate` → Xcode 열기 → Build**
4. **Day 1 Korean IME 검증** (가장 중요)
5. **결과 보고** — 통과/실패 & 다음 단계 결정

---

## 0. 사전 요구사항 / Prerequisites

| 항목 | 요구 | 확인 방법 |
|---|---|---|
| macOS | **26.0 (Tahoe) 이상** | `sw_vers -productVersion` |
| Xcode | **16.0 이상** (deploymentTarget 26.0 지원) | `xcodebuild -version` |
| xcodegen | 최신 (Homebrew 권장) | `brew install xcodegen` 또는 `xcodegen --version` |
| Apple Developer Team ID | 무료 계정도 가능 (notarization 만 유료 $99/년) | <https://developer.apple.com/account> → Membership → Team ID |

---

## 1. 저장소 클론 / Clone

```bash
cd ~/Workspace   # 또는 적당한 작업 디렉토리
git clone https://github.com/Demian-Yim/flow-zoomit-mac.git
cd flow-zoomit-mac
```

---

## 2. Team ID 설정 / Set Apple Developer Team ID

`src/project.yml` 안의 두 곳에 있는 `REPLACE_WITH_YOUR_TEAM_ID` 를 본인 Team ID 로 바꿉니다 (10자, 예: `ABC123XYZ7`).

```bash
# Team ID 가 ABC123XYZ7 라고 가정
sed -i '' 's/REPLACE_WITH_YOUR_TEAM_ID/ABC123XYZ7/g' src/project.yml
```

또는 텍스트 편집기로 직접 두 곳 수정.

> ⚠️ **이 변경은 commit 하지 마세요** — 본인 ID 가 노출됩니다. 빌드만 하고 그대로 두거나, 커밋 전 되돌리세요.

---

## 3. Xcode 프로젝트 재생성 + 빌드 / Regenerate & Build

```bash
make generate    # src/project.yml → src/ZoomacIt.xcodeproj 재생성
make build       # Debug 빌드 (build/ 에 결과)
make run         # 빌드 + 앱 실행 (메뉴바에 아이콘이 나타남)
```

**예상 결과:**
- 메뉴바 우상단에 FLOW ZoomIt 아이콘 등장
- 첫 실행 시 macOS 가 "Screen Recording" 권한 요청 → **System Settings → Privacy & Security → Screen Recording** 에서 활성화 후 앱 재시작

---

## 4. Day 1 Korean IME 검증 ⭐ (가장 중요)

이 검증이 **FLOW ZoomIt for Mac 프로젝트 전체의 게이트**입니다. 통과하면 v0.1 진행, 실패하면 대안 경로(Magnify 협업 / Presentify 가이드)로 전환.

### 검증 절차

1. 메뉴바 아이콘 → 앱 활성 확인
2. `⌃2` → 그리기 모드 진입 (화면이 살짝 어두워지고 캔버스 모드)
3. `T` → 텍스트 모드 활성
4. 캔버스의 빈 공간 클릭 → 텍스트 커서 등장
5. **`한/영` 키 (또는 Caps Lock 으로 매핑된 IME 토글) → 한국어 IME 활성**
6. **두벌식으로 입력 — 예: `dkssudgktpdy`** → 화면에 `안녕하세요` 가 자연스럽게 조합되며 표시되는지 확인
7. 입력 중 조합 (한 글자씩 만들어지는 모습) 이 정상인지 확인 — 예: `ㅇ` → `아` → `안` → `안ㄴ` → `안녀` → `안녕`
8. `Enter` 키 또는 `Esc` 키 → 텍스트 commit (캔버스에 라스터화)

### 결과 분기

| 결과 | 의미 | 다음 단계 |
|---|---|---|
| ✅ **자연스러운 한글 조합 + commit 정상** | 핵심 가설 통과! | v0.1 진행 → DMG 빌드 → 시범 |
| ⚠️ **글자 조합은 되는데 commit 시 깨짐** | 라스터화 단계 폰트 이슈 | TextInputController.rasterizeAndComposite 의 폰트 처리 점검 |
| ❌ **글자 자체가 입력 안 되거나 영문으로만 입력** | NSTextView IME 비양립 (예상 외) | 프로젝트 전환 검토 (Magnify / Presentify) |
| ❌ **앱이 크래시** | 환경 호환성 이슈 | 로그 확인 후 보고 |

### 검증 시 화면 캡처

가능하면 **녹화로 입력 과정 전체** 를 남겨주세요 (QuickTime 또는 ⌘⇧5). v0.1 ADR 에 첨부합니다.

---

## 5. 손글씨 폰트 검증 / Handwriting Font Test

기본 fallback 은 `Apple SD Gothic Neo Bold` 입니다 (macOS 기본 설치 폰트). 검증 후 본인이 좋아하는 한국어 손글씨 폰트로 바꿔보세요:

1. 앱 메뉴바 아이콘 → Settings...
2. (UI 에 Font Family 필드가 추가되어야 함 — v0.1 추가 작업 필요. 임시로는 **defaults write 명령** 으로 설정)
   ```bash
   # 예: 나눔바른펜 Bold 적용 (시스템에 설치되어 있어야 함)
   defaults write kr.flowdesign.ZoomacIt textDefaultFontFamily "NanumBarunpenB"
   # 또는 Pretendard
   defaults write kr.flowdesign.ZoomacIt textDefaultFontFamily "Pretendard-Bold"
   ```
3. 앱 재시작 → ⌃2 → T → 캔버스 클릭 → 한글 입력 → 폰트가 적용되는지 확인

**참고:** 시스템에 폰트가 없으면 자동으로 `Apple SD Gothic Neo Bold` 로 fallback 됩니다. 추가로 fallback 하려면 시스템 폰트.

---

## 6. 6색 펜 전환 / Color palette test

1. ⌃2 → 그리기 모드
2. R / G / B / Y / O / P 키 차례로 누르며 펜 색이 변하는지 확인
3. 각 색상으로 자유 펜 그리기 → 색이 정확히 표시되는지

---

## 7. 결과 보고 / Reporting back

검증 후 아래 양식으로 결과를 알려주세요:

```
환경:
- macOS 버전: (예: 26.1)
- Xcode 버전: (예: 16.2)
- Mac 모델: (예: MacBook Pro 14" M3, 2024)

Day 1 IME 검증:
- 한글 조합: ✅ / ⚠️ / ❌
- 한글 commit: ✅ / ⚠️ / ❌
- 화면 녹화 첨부 여부: 예 / 아니오

손글씨 폰트:
- defaults write 후 폰트 적용: ✅ / ⚠️ / ❌
- fallback (Apple SD Gothic Neo) 동작: ✅ / ⚠️ / ❌

6색 펜:
- R/G/B/Y/O/P 모두 정상: ✅ / ⚠️ / ❌

추가 발견:
- (예상치 못한 문제, 좋은 점, 개선 제안 등)
```

---

## 8. 다음 단계 / What's next

### IME 통과 시 (예상 시나리오)
- v0.1.0 태그 + GitHub Release
- DMG 빌드 (`make dmg VERSION=0.1.0`)
- README 에 macOS 스크린샷 추가
- HF Spaces 정적 사이트 (`flow-zoomit-mac`)
- Notion 백업
- v0.2 로드맵 — Settings UI 의 폰트 패밀리 입력 필드, B/W 안전 다이어그램 macOS 버전, Live Zoom (현재 ZoomacIt 미구현)

### IME 실패 시 (예외 시나리오)
- 즉시 보고 → 분석
- 대안 1: NSTextView 가 아닌 자체 IME 핸들링 (복잡)
- 대안 2: [Magnify](https://github.com/jayleekr/Magnify) 협업 (한국 개발자 프로젝트)
- 대안 3: Presentify (유료 상용) 가이드만 작성

---

## 부록: 코드 변경 요약 (FLOW 포크에서 추가된 부분)

| 파일 | 변경 |
|---|---|
| `src/ZoomacIt/Models/Settings.swift` | `defaultFontFamily` 키·프로퍼티 추가 / `resolveFont(size:)` 헬퍼 추가 / 기본 폰트 가중치 `medium` → `bold` |
| `src/ZoomacIt/Draw/TextInputController.swift` | `NSFont.systemFont(...)` 3곳 → `Settings.shared.resolveFont(size:)` 로 교체 |
| `src/project.yml` | `bundleIdPrefix` `com.x07jp27` → `kr.flowdesign` / `PRODUCT_NAME` → `FLOW ZoomIt` / `DEVELOPMENT_TEAM` placeholder |
| `src/ZoomacIt/Resources/Info.plist` | `CFBundleDisplayName` 추가 (FLOW ZoomIt) / `CFBundleLocalizations` 추가 (en, ko) / `NSScreenCaptureUsageDescription` 다국어 / `NSHumanReadableCopyright` 추가 |
| `README.md` | 갈아엎음 — FLOW 브랜딩 + 다국어 + 크레딧 |
| `README_ko.md` | 신규 — 한국어 우선 |
| `docs/MAC_BUILD_HANDOFF.md` | 본 문서 |

원본 ZoomacIt 코드 (Draw, Overlay, Core, App, Settings UI) 는 **그대로 유지** — 업스트림 fetch & merge 가 깔끔하게 동작합니다.

---

© 2026 FLOW: AX 디자인연구소 · 본 문서는 fork 산출물. 업스트림 ZoomacIt 의 모든 GPL-3.0 의무 준수.
