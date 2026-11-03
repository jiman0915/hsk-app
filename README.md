# HSK4 단어장 안드로이드 앱

웹 단어장을 Capacitor 7로 감싼 안드로이드 앱이야. 빌드는 GitHub Actions가 클라우드에서 해주니까 PC에 Android Studio를 깔 필요 없어.

- 앱 ID: `com.fieldwise.hsk4` (한 번 올리면 못 바꿔)
- 대상: Android 6.0 이상, targetSdk 35 (구글 플레이 현재 요구사항 충족)
- 발음: 기기의 중국어 TTS 사용 (안 나오면 폰 설정 > 텍스트 음성 변환에서 중국어 음성 설치)

## 1단계. GitHub에 올리기 (10분)

1. GitHub에서 새 저장소 만들기: 이름 `hsk-app`
2. 이 폴더 내용을 전부 올리기 (`.github` 폴더 포함)
   - 웹에서 올릴 땐 "uploading an existing file"에 폴더째 드래그
3. 저장소 **Settings → Secrets and variables → Actions → New repository secret** 에 4개 추가
   - `KEYSTORE_BASE64` : `hsk4-upload.jks.base64` 파일 내용 전체
   - `KEYSTORE_PASSWORD` : `secrets.txt`에 있는 값
   - `KEY_PASSWORD` : `secrets.txt`에 있는 값
   - `KEY_ALIAS` : `hsk4`
4. **Actions 탭 → Android build → Run workflow** (버전 이름 1.0.0)
5. 10분쯤 뒤 완료되면 아래 두 파일이 생겨
   - `hsk4-test-apk` : 폰에 바로 깔아서 테스트하는 파일
   - `hsk4-playstore-aab` : 플레이 스토어에 올리는 파일

> 서명 키(`hsk4-upload.jks`)랑 비밀번호는 **절대 잃어버리면 안 돼.** 구글 드라이브 같은 안전한 곳에 따로 백업해둬. 저장소에는 올리지 마.

## 2단계. 폰에서 먼저 테스트

1. `hsk4-test-apk` 다운로드 → 압축 풀기 → `app-debug.apk`를 폰으로 옮겨 설치
2. 확인할 것: 카드 넘기기, 🔊 발음, 획순·써보기, 시험·오답노트, 앱 껐다 켜도 진도 남아있는지

## 3단계. 플레이 콘솔 등록

1. https://play.google.com/console 가입 (1회 $25, 본인 인증 1~2일)
   - 개인 계정은 **테스터 12명이 14일 연속 비공개 테스트**를 해야 프로덕션 공개가 열려.
2. 앱 만들기 → 앱 이름 `HSK4 단어장`, 기본 언어 한국어, 앱, 무료
3. 앱 콘텐츠 작성
   - 개인정보처리방침 URL: 저장소 Settings → Pages에서 `main` 브랜치 `/docs` 켜면 `https://jiman0915.github.io/hsk-app/privacy.html`
   - 광고: 없음 / 데이터 보안: 수집·공유 없음 / 대상 연령: 13세 이상 / 콘텐츠 등급 설문
4. 스토어 등록정보: `docs/store-listing.md` 문구, 아이콘 `assets/icon-only.png`(512px로 자동 축소), 그래픽 `docs/feature-graphic.png`, 스크린샷 `docs/screenshots/1~4`
5. 테스트 → 비공개 테스트(또는 프로덕션) → 새 버전 만들기 → `app-release.aab` 업로드 → 검토 제출

## 업데이트할 때

`www/` 안의 파일을 바꾸고 커밋하면 Actions가 자동으로 새 빌드를 만들어. 버전 코드는 자동으로 올라가니까 새 AAB만 플레이 콘솔에 올리면 돼.
