# 검증 결과 — 2026-11-05 KST

## 통과

- Release APK 빌드, Android Lint: 오류 0 / 경고 0.
- 로컬 배포 전용 키 서명. 디버그 서명이 아니며 APK 디버깅 비활성화.
- 순수 Java 테스트: RSSI 유효 범위, −127 오류값, dBm/아이콘 부호 변환, 3자리 값, 주파수 대역, 연결 해제 시 이전 숫자 제거.
- Android 15(API 35) AOSP arm64 에뮬레이터: 배포 APK 설치·실행.
- 위치/접근성 권한 없이 에뮬레이션된 Wi-Fi RSSI −50 dBm 조회.
- Android 알림 권한 요청 → 허용 → 포그라운드 서비스 시작.
- 상태 표시줄 숫자 50 및 알림창 −50 dBm 표시 확인.
- 런처 위젯 추가, 값·주파수 대역·마지막 측정 시각·버튼 렌더링 확인.
- Wi-Fi OFF 시 위젯과 알림이 — dBm / Wi-Fi 꺼짐으로 전환.
- 알림의 측정 중지 클릭 후 MonitorService 종료 확인.
- 최종 레이아웃 수정 APK 업데이트 설치.
- 서비스 중지 후 위젯 새로고침으로 재연결된 Wi-Fi의 −50 dBm 조회.
- 테스트 중 AndroidRuntime 오류 로그 없음.

## 아직 확인하지 않은 사항

- Galaxy Z Fold7 / One UI 9.0 설치, 알림 아이콘 가독성, 런처 위젯 크기.
- Google Play 프로텍트 판정: AOSP 에뮬레이터에 Google Play 서비스가 없으므로 검증하지 못함.
- 실제 이동 중 신호 변화, Wi-Fi 7/MLO, VPN, 여러 물리 Wi-Fi 연결.
- 장시간 절전/백그라운드 제한/재부팅/폴드 화면 전환.

`qa/`에 에뮬레이터 실행 화면이 있습니다. −50 dBm은 에뮬레이터가 보고한 값이며 실제 폴드7 측정 결과가 아닙니다.

## 0.2.0-alpha 추가 검증

- 동일 배포 키 / versionCode 2로 기존 0.1 위에 업데이트 설치 성공.
- 5단계 구간 모든 경계값(-81/-80, -71/-70, -61/-60, -51/-50), 서로 다른 5색 및 연결 해제 중립 단계 테스트 통과.
- Android Lint 오류 0 / 경고 0.
- 에뮬레이터 알림창에서 하늘색 50 숫자 배지 및 매우강함 표시 확인. 상태 표시줄은 시스템 단색 유지.
- 4개 위젯 공급자 등록 확인. 기존 상세 위젯 유지, 새 미니·기본·와이드 추가 성공.
- 새 위젯 표시 화면은 qa/v02-home-*.png, 알림은 qa/v02-notification.png.
- 5색 모두의 실제 무선 신호 변화 및 One UI 런처의 크기 배치는 실기기 추가 확인 필요.

## 0.3.0-alpha 검증

- 기존 앱 위 업데이트 설치 성공, 동일 서명 / versionCode 3.
- Android Lint 오류 0 / 경고 0.
- 퍼센트 환산 경계와 상·하한, 연결 해제 중립 표시 테스트 통과.
- Wi-Fi 규격 매핑 테스트: 11ac→5, 11ax→6/6E, 11be→7, 11ad→WiGig, 미확인 값을 주파수로 추측하지 않음.
- 에뮬레이터 런처 추가 화면에서 새 위젯 기본 크기 1×1 / 2×1 / 3×2 각각 확인.
- 기존 위젯은 이전 점유 칸 수를 유지하는 현상도 확인. 제거 후 재추가 안내 필요.
- 상태 표시줄 100 및 알림창 100% / −50 dBm 표시 확인.
- 정확한 위치 고지/권한 요청 → 허용 → 실제 에뮬레이터 스캔 결과 AndroidWifi / −50 dBm 수신 확인.
- 큰 위젯에서 주변 목록과 숫자 표시 확인. 최근 검색임을 표시하고 캐시 표시 수명은 5분.
- 위젯의 시각 텍스트 제거, 실제 연결 2.4 GHz 및 구형 802.11a/b/g 표시 확인. 작은 위젯은 구형 Wi-Fi로 축약.
- 3×2 위젯 터치 → 앱 열기 확인.
- 1×1 중앙 배치 개선 및 최소 높이 48dp 적용. 2×1의 최소 높이는 이전 76dp에서 40dp로 감소.

미검증: Galaxy One UI의 실제 격자/폰트 크기별 배치, 실제 Wi-Fi 5/6/7 AP 접속, 다중 AP 및 MLO, 오래 실행할 때 배터리 영향. 핀치투줌은 지원하지 않으며 런처의 길게 누르기/테두리 리사이즈를 사용합니다.

최종 설치본에서 새 1×1 및 2×1 위젯도 각각 터치해 MainActivity가 열리는 것을 확인했습니다. 최종 테스트 중 AndroidRuntime 오류 로그가 없었습니다.

## 0.4.0-alpha (2026-11-05)

- Removed numeric status notification and foreground service; no notification permission remains.
- Release build / lint successful. Usage Access manifest lint suppression is limited to PACKAGE_USAGE_STATS: it is granted through the documented user-controlled app-op settings flow.
- Signal calculation regression main passed (RSSI bounds, percentage/levels, bands, Wi-Fi generations).
- API 35 emulator: existing signing-key update installs; all widget sizes render percentage, dBm and mobile usage; opacity slider changed 90% → 50%; large metric text increased, list rows compact.
- Usage Access settings route verified. Before grant: permission needed. After app-op grant: real OS aggregate 66.2 KB shown for today and this month. Device has only today's records, so values match; actual carrier/dual-SIM billing accuracy not tested.
- Periodic job 40 registered, forced background execution completed and returned to waiting. This tests job execution, not a full overnight/Doze or naturally elapsed 30-minute cadence.
- Wi-Fi list scanned AndroidWifi at −50 dBm. ACTION_WIFI_ADD_NETWORKS reached Android Settings (ActivityTaskManager log); emulator returned immediately for its existing virtual network. Result handling offers Wi-Fi settings. A new external AP connection and secured-password entry require physical-device testing.
- No AndroidRuntime crashes in smoke test. APK v2 signature verified.
- Screenshots: qa/v04-ready-small.png and qa/v04-ready-home-0.png. Older shots may show intermediate layouts.
- Galaxy Z Fold7 / One UI 9, actual Wi-Fi 6/7 APs, carrier statistics, background-location grant via Samsung UI and battery-policy behavior remain physical-device checks.

## 0.5.0-alpha (2026-11-05)

- Release build and lint passed (no issues). Signal regression test passed.
- Shared RemoteViews renderer is used by installed widgets and the in-app preview. Preview size buttons, 0% opacity and 140% font setting exercised on API 35 emulator; no AndroidRuntime errors.
- Daily and monthly mobile statistics stored separately. Selected monthly in the app, confirmed all launcher widgets still say 오늘 with daily bytes.
- Widget AndroidWifi row tap reached the Android network-save result flow for that exact SSID, while normal widget root retains app-open behavior. Cached network name is validated before handling; intent payload is consumed once.
- Installed 0.5 over 0.4 using the same distribution key. APK v2 signature verified.
- Screenshots: qa/v05-preview-final.png, qa/v05-widget-final.png, qa/v05-transparent-largefont.png, qa/v05-widget-selection.png.
- Real Samsung launcher sizes and accessibility font settings may differ. Network approval/password behavior on new physical APs and actual carrier usage accuracy remain device tests; automatic scan scheduling constraints are unchanged.

## 0.6.0-alpha (2026-11-05)

- Data captions: 1×1 데이터; 2×1 and 3×2 데이터 사용량. Renderer reads the app-selected today/month value, and accessibility description includes that period. Daily/monthly caches remain separate.
- Small-widget dBm badge / separate data panel rendered in launcher and preview on API 35; existing-key APK update installed. No AndroidRuntime errors during smoke test.
- WifiSecurityTest passes for open, OWE, WPA2, WPA3, transition, enterprise, WEP, unknown/legacy, and password length/character rules. Security type persisted separately from the old secured flag; old cache defaults to unsupported until scanned again.
- Personal WPA2/WPA3 password dialog added. Values are cleared on dismiss/submit, not persisted or logged; dialog uses FLAG_SECURE and disables autofill/view state saving. Enterprise/legacy/unknown offers system settings.
- Emulator open AndroidWifi selection reached successful system save-result handling. Secured physical-AP password dialog and actual WPA2/WPA3 association remain real-device validation; no unsupported claim of silent device-wide switching.
- Release build and lint passed; same distribution signing key retained. Screenshots qa/v06-tiny.png, v06-compact.png, v06-widgets.png.

## 0.7.0-alpha (2026-11-05)

- Build and lint pass (no issues); APK v2 signature verified.
- Added non-exported ConnectActivity with floating, translucent dialog theme, separate task affinity and excludeFromRecents. Widget row PendingIntent targets it directly; MainActivity delegates app-list selection to the same screen.
- API 35 emulator update test: widget AndroidWifi tap showed 선택한 Wi-Fi, AndroidWifi, OPEN / −50 dBm and system save result in ConnectActivity; no MainActivity content. Activity dump confirmed separate translucent connection task. Closing returned to launcher; no AndroidRuntime crashes.
- Existing user-launched emulator-5554 was used after separate emulator launch was blocked by the active AVD. It was left running after tests.
- SSID is shown without single-line truncation, in input and result states. Password is not saved across recreation; pending/outcome state is saved to avoid automatic resubmission after rotation.
- Password fields and popups use FLAG_SECURE. Physical WPA2/WPA3 authentication remains a device test; open-network popup lifecycle was tested on the emulator.

## 0.8.0-alpha (2026-11-05)

- Added `이미 저장한 Wi-Fi · 시스템에서 연결` immediately beneath the selected SSID, with guidance to choose that SSID in system settings. Available before password entry and in result/fallback states; any typed password is cleared before leaving.
- Release build, lint (no issues), APK signature verification passed.
- API 35 update test: widget → AndroidWifi popup displayed the new button and explanatory text; tapping it opened com.android.settings Wi-Fi list containing AndroidWifi. No AndroidRuntime crashes.
- Existing test emulator left running. No new permissions or claim of automatic saved-network detection/direct connection.

## 0.9.0-alpha (2026-11-05)

- Rounded background now uses the system widget radius (clamped for very small bounds), with 2dp edge clearance and an additional half-stroke inset. Fill and stroke arcs share a consistent outer boundary.
- Rasterization follows screen density, capped at approximately 350,000 pixels per widget; background alpha and gradient retained.
- Small-widget data panel radius increased to keep its fill inside the outer curve.
- Release build / lint passed, update install and signature verified. API 35 launcher screenshots inspected for all sizes; no AndroidRuntime errors in initial smoke test. Final screenshot: qa/v09-widget-corners-final.png.
- Galaxy Z Fold7 / One UI clipping must still be confirmed on the user's launcher. Existing emulator left running.


## 0.10.0-beta.2 (2026-11-05)

- App name: 디스커넥트 제로. Description clarifies monitoring, not guaranteed disconnection prevention; Korean signal terminology normalized to 신호 강도.
- Nearby scan cache preserves frequency and standard; widget/app rows show Android-reported band/generation. Emulator scan standard is unknown and correctly displayed as 규격 미확인 rather than guessed.
- Transparent Wi-Fi + −50 dBm vector launcher icon; no background rectangle. Separate monochrome update notification icon.
- Medium/large widgets use horizontal insets up to 16dp and vertical 12dp, reduced only for unusually short bounds. Android-rendered 250×110dp and 310×240dp captures inspected: text and data remain inset and legible. qa/beta2-medium.png, beta2-large.png, beta2-icon.png.
- Release build, Android Lint (no issues), same-key update installation passed on API 35 emulator.
- Pure Java regression tests passed for signal thresholds/bands/generations, Wi-Fi authentication/password rules, version ordering (numeric prerelease identifiers), draft/incomplete assets, stable/beta ordering, same/older releases, official repository APK URL constraints.
- Separate Android instrumentation APK (not distributed) passed live GitHub API request, JobScheduler enable/disable, posting a new-version notification with permission, saving notification dedup state, restoring original preferences, and widget/icon rendering. Synthetic v99 fixture is test-only, was never published/downloaded, and was removed after the check.
- Update checks use the public ZERO-hms/disconnect-zero release list, including prereleases. Daily scheduling is approximate; the test forced execution, not a naturally elapsed day/Doze cycle.
- Ordinary installs require the user's Android confirmation. Full browser-to-installer upgrade on Galaxy One UI 9, Play Protect evaluation, and real carrier/AP behavior remain device checks.
