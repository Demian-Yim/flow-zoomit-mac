---
title: FLOW ZoomIt for Mac
emoji: 🍎
colorFrom: pink
colorTo: indigo
sdk: static
pinned: false
license: gpl-3.0
short_description: Korean-friendly ZoomacIt fork for macOS lecturers
---

# FLOW ZoomIt for Mac

> A Korean-friendly distribution of [**ZoomacIt**](https://github.com/07JP27/ZoomacIt) — a native macOS menu bar app inspired by Microsoft Sysinternals ZoomIt for Windows. Bundled with Korean handwriting font defaults, opinionated FLOW pen presets, and bilingual UX. Built for Korean trainers, coaches, and presenters.
>
> 한국어 강의·워크숍·코칭을 위한 [ZoomacIt](https://github.com/07JP27/ZoomacIt) 기반의 macOS 메뉴바 앱. 손글씨 폰트·FLOW 펜 기본값·양국어 UX 포함. ZoomIt for Windows 의 Mac 호환판.

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-GPL--3.0-blue?style=flat" alt="License: GPL-3.0"></a>
  <img src="https://img.shields.io/badge/Swift-6.0-orange?style=flat&logo=swift&logoColor=white" alt="Swift 6.0">
  <img src="https://img.shields.io/badge/macOS-26%2B-blue?style=flat&logo=apple&logoColor=white" alt="macOS 26+">
  <img src="https://img.shields.io/badge/status-v0.1%20fork-yellow?style=flat" alt="v0.1 fork">
</p>

🇰🇷 [한국어 README →](README_ko.md)
🇯🇵 Original Japanese: [README_ja.md](README_ja.md)

---

## Why this fork? / 왜 포크했나

The Windows side of FLOW ZoomIt (Sysinternals v11.0 + Korean handwriting font + 6-color palette) lives at <https://github.com/Demian-Yim/flow-zoomit>. macOS users were left out — Microsoft never ported ZoomIt to Mac. This project picks up the excellent open-source [ZoomacIt](https://github.com/07JP27/ZoomacIt) (Swift 6 + AppKit, by [@07JP27](https://github.com/07JP27)) and re-skins it with the same Korean classroom defaults: handwriting font preset, full pen palette, bilingual docs, and the B/W canvas-blank safety guidance.

Windows 쪽 [FLOW ZoomIt](https://github.com/Demian-Yim/flow-zoomit) 의 macOS 짝꿍이 없어서 만든 포크. Microsoft 가 ZoomIt 을 Mac 으로 포팅하지 않았기 때문에, [@07JP27](https://github.com/07JP27) 의 훌륭한 오픈소스 [ZoomacIt](https://github.com/07JP27/ZoomacIt)(Swift 6 + AppKit)을 베이스로 한국어 강의 디폴트(손글씨 폰트·6색 펜 팔레트·양국어 문서·B/W 안전 가이드)를 입혔습니다.

---

## ⚠️ Status: source fork — no .dmg yet / 소스 포크 단계 — 다운로드용 .dmg 없음

> **솔직하게 말씀드립니다.** 이 저장소는 현재 **소스 코드 포크 단계**입니다. 다운로드 가능한 빌드는 아직 없습니다.

**✅ 완료 / Done:**
- ZoomacIt 포크 완료 / Forked ZoomacIt
- FLOW 한국어 디폴트 적용 — 손글씨 폰트 fallback chain, 펜 굵기, 6색 팔레트 / FLOW Korean defaults — handwriting-font fallback chain, pen width, 6-color palette
- Bundle ID + project.yml + 양국어 문서 / Bundle ID, project.yml, bilingual docs

**⏳ 아직 검증 안 됨 / Not yet verified:**
1. **macOS 에서 실제 컴파일·실행** / Actual compile & run on macOS
2. **한글 IME 검증** — `NSTextView` 가 투명 캔버스 안에서 한글 조합을 정상 처리하는지 / Korean IME validation in `NSTextView` (the gating test)
3. **빌드·서명·notarization** / Build, code-signing, Apple notarization
4. **`.dmg` 패키징** / `.dmg` packaging

**현재 다운로드 가능한 빌드는 없습니다.** Windows 버전이 안정화된 후 Mac 환경에서 Day-1 검증을 통과해야 v0.1 .dmg 가 나옵니다. 진행 상황을 보시려면 GitHub Watch 를 추천합니다.

**No downloadable build exists yet.** Once the Windows version stabilizes, Day-1 verification on Mac must pass before v0.1 .dmg ships. Watch this repo for progress.

See [docs/MAC_BUILD_HANDOFF.md](docs/MAC_BUILD_HANDOFF.md) for the step-by-step build & validation guide on macOS.
Mac 에서의 단계별 빌드·검증 가이드는 [docs/MAC_BUILD_HANDOFF.md](docs/MAC_BUILD_HANDOFF.md) 참조.

---

## 📖 만든 이의 이야기 / Maker's note

반갑습니다. **FLOW: AX 디자인연구소** 임정훈 소장입니다. Windows 용 [FLOW ZoomIt](https://github.com/Demian-Yim/flow-zoomit) 을 만든 후 "맥북용도 만들어 주세요" 라는 요청을 여러 차례 받았습니다.

Microsoft 는 ZoomIt 을 macOS 로 포팅하지 않았습니다. 마침 [@07JP27](https://github.com/07JP27) 님의 오픈소스 [ZoomacIt](https://github.com/07JP27/ZoomacIt) (Swift 6 + AppKit 네이티브) 이 ZoomIt 의 정신적 클론으로 활발히 개발 중이어서, GPL-3.0 라이선스로 포크해 **한국어 강의 디폴트**를 입히는 방향으로 진행하고 있습니다.

Windows 버전 개발 과정에서 Electron + 자체 IME 로 5번 시도했다가 모두 실패했던 경험이 있어, Mac 에서도 **Day 1 한글 IME 검증**을 먼저 통과한 뒤 본격 빌드에 들어갑니다. 시간이 좀 걸리더라도 한국어 입력이 정상 작동하는 빌드만 내놓으려고 합니다.

📜 Windows 버전 전체 후기: [STORY.md](https://github.com/Demian-Yim/flow-zoomit/blob/main/STORY.md)

Hi, I'm **Demin Yim** (Yim Jeonghun), Director of **FLOW: AX Design Lab**. After releasing the Windows-only [FLOW ZoomIt](https://github.com/Demian-Yim/flow-zoomit), several Korean trainers asked for a Mac equivalent. Microsoft never ported ZoomIt to macOS, so I'm forking [@07JP27](https://github.com/07JP27)'s [ZoomacIt](https://github.com/07JP27/ZoomacIt) under GPL-3.0 with FLOW Korean defaults.

During the Windows build I burned five Electron prototypes with custom Korean IMEs — all failed because transparent Chromium windows are incompatible with Hangul composition. So for the Mac fork I'm deliberately gating on Day-1 Korean IME verification. A working Korean input is non-negotiable.

---

## What's different from upstream ZoomacIt / 원본과의 차이

| | ZoomacIt (upstream) | **FLOW ZoomIt for Mac** |
|---|---|---|
| Default font weight | Medium | **Bold** (Korean handwriting tone) |
| Default font family | System default | **Configurable** — falls back to `Apple SD Gothic Neo Bold` (Korean), then system font |
| Bundle ID prefix | `com.x07jp27` | `kr.flowdesign` |
| Display name | `ZoomacIt` | `FLOW ZoomIt` |
| Documentation | English / Japanese | **Korean / English** (Japanese kept as `README_ja.md`) |
| B/W canvas-blank safety | — | **Bilingual safety guidance** (translated from Windows v1.0.1) |
| Creator credit | 07JP27 | 07JP27 (upstream) + FLOW: AX 디자인연구소 (fork) |

### What's the same

Everything else — feature set, hotkeys (⌃1 zoom · ⌃2 draw · ⌃3 break timer), 6-color palette (R/G/B/Y/O/P, with pink), shape modifiers (Shift = arrow, Control = rect, Tab = ellipse, Shift+Control = line), Carbon `RegisterEventHotKey` mechanism, 3-layer canvas compositing.

---

## Hotkeys / 단축키

| Key | Action / 동작 |
|---|---|
| `⌃1` | Static Zoom / 정적 줌 |
| `⌃2` | Draw mode / 그리기 모드 |
| `⌃3` | Break Timer / 휴식 타이머 |

### Draw-mode shortcuts / 그리기 모드 단축키

| Key | Action |
|---|---|
| `R G B Y O P` | Pen color: Red Green Blue Yellow Orange Pink |
| `Drag` | Free-pen stroke / 자유 펜 |
| `Shift+Drag` | Arrow / 화살표 |
| `Control+Drag` | Rectangle / 사각형 |
| `Tab+Drag` | Ellipse / 타원 |
| `Shift+Control+Drag` | Straight line / 직선 |
| `Wheel` | Adjust pen width / 펜 굵기 |
| `T` | Text mode / 텍스트 모드 |
| **`B`** | ⚠️ Blank black canvas — `⌘Z` to undo / 검정 덮어쓰기, ⌘Z 로 취소 |
| **`W`** | ⚠️ Blank white canvas — `⌘Z` to undo / 흰 덮어쓰기, ⌘Z 로 취소 |
| `E` | Erase all / 전체 지우기 |
| `⌘Z` | Undo / 되돌리기 |
| `Esc` | Exit draw mode / 그리기 종료 |

### ⚠️ Korean text input safety / 한글 입력 시 주의

**Same gotcha as Windows:** in Draw mode, a standalone `B` or `W` keystroke blanks the canvas. If you press `한/영` to switch to Korean **before** pressing `T` to enter text mode, the first Hangul jamo can trigger this — `w` is `ㅈ` (자/저/주) and `b` is `ㅠ` in 두벌식.

**Safe order:** `⌃2` → **`T` first** → click canvas → `한/영` → type Korean
**Recovery:** `⌘Z` once

(See Windows v1.0.1 release notes for the full backstory: <https://github.com/Demian-Yim/flow-zoomit/releases/tag/v1.0.1>)

---

## License / 라이선스

**GPL-3.0** — inherited from upstream [ZoomacIt](https://github.com/07JP27/ZoomacIt). Source code public on GitHub. See [LICENSE](LICENSE).

GPL-3.0 — 업스트림 ZoomacIt 에서 상속. 소스 코드 GitHub 에 공개. 라이선스 변경 불가.

### Credits / 크레딧

- **Upstream / 원작:** [ZoomacIt by 07JP27](https://github.com/07JP27/ZoomacIt) — Swift 6 / AppKit native macOS menu bar app inspired by Sysinternals ZoomIt. All core engineering credit goes here.
- **FLOW fork / FLOW 포크:** [FLOW: AX 디자인연구소 / FLOW: AX Design Lab](https://flowdesign.ai.kr) by **임정훈 소장 · Demin Yim**, Director · AI Coordinator. Korean-classroom defaults, bilingual UX, FLOW branding.
- **Inspiration / 영감:** Microsoft Sysinternals ZoomIt for Windows — the original screen-annotation tool that made every classroom presenter's life easier for 20+ years.

---

## Related projects / 관련 프로젝트

- **Windows version**: <https://github.com/Demian-Yim/flow-zoomit> — ships Microsoft Sysinternals ZoomIt v11.0 with FLOW Korean defaults

---

© 2026 FLOW: AX 디자인연구소 · FLOW: AX Design Lab — fork content. Upstream code © 2025–2026 07JP27 (GPL-3.0).
