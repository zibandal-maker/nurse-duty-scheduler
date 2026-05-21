# 🚀 배포 가이드 (Step by Step)

이 문서는 박 선생님 도구를 **인터넷에 배포**하는 전체 과정입니다.
순서대로 따라하시면 약 **1~2시간** 안에 배포가 완료됩니다.

---

## ✅ 사전 준비 (계정 가입)

다음 4개 계정만 있으면 됩니다. 모두 무료입니다.

| 서비스 | 용도 | URL |
|---|---|---|
| **GitHub** | 코드 저장 | github.com |
| **Vercel** | 호스팅 | vercel.com |
| **Formspree** | 피드백 수집 | formspree.io |
| **Buy Me a Coffee** | 후원 (선택) | buymeacoffee.com |

추가로 한국 후원용:
- **토스 송금 링크**: 토스 앱 → 송금 링크 (이미 토스 사용 중이면 즉시 생성)
- **카카오페이 QR**: 카카오페이 앱 → QR결제 → 송금받기

---

## 📁 Step 1. 파일 준비

이 폴더의 다음 파일들이 배포 대상입니다:

```
index.html          ← 메인 도구
manifest.json       ← PWA 메타데이터
service-worker.js   ← 오프라인 캐싱
icon-192.png        ← 앱 아이콘 (작음)
icon-512.png        ← 앱 아이콘 (큼)
vercel.json         ← Vercel 캐시 설정
README.md           ← 저장소 설명
LICENSE             ← MIT 라이선스
.gitignore          ← Git 제외 파일
```

---

## 📝 Step 2. 플레이스홀더 교체

**이 단계가 가장 중요합니다.** `index.html`의 다음 부분을 본인 정보로 바꿔야 합니다.

### 2-1. Formspree 엔드포인트 (선택 — 안 해도 동작합니다)

**기본 동작**: 사용자가 피드백 보내면 사용자의 메일 앱이 자동으로 열리고, 박 선생님 이메일(`zibandal@gmail.com`)로 보내집니다. **추가 설정 없이 그대로 동작**합니다.

**Formspree 설정 시 장점**: 메일 앱이 안 열리고 도구 안에서 바로 전송됩니다. 사용자 경험이 매끄럽고, 통계도 볼 수 있습니다.

설정하려면:
1. [formspree.io](https://formspree.io)에서 가입 (Gmail OAuth 가능)
2. 우상단 "+ New Form" 클릭
3. Form name 입력 (예: "Duty Scheduler Feedback"), 등록 이메일에 **zibandal@gmail.com** 입력
4. 생성되면 `https://formspree.io/f/abcdEFGH` 같은 URL이 나옴

`index.html`을 텍스트 에디터로 열고 검색(Ctrl+F):

```
REPLACE_WITH_YOUR_FORM_ID
```

이 부분을 본인 폼 ID로 교체:

```js
// After (예시)
var FORMSPREE_ENDPOINT = 'https://formspree.io/f/abcdEFGH';
```

무료 플랜: 월 50건. 초과 시 다음 달 1일 리셋.

### 2-2. 후원 링크 (선택 — 카카오페이 QR 사용)

박 선생님은 **카카오페이 QR 이미지(`kakaopay-qr.png`)**로 후원을 받습니다. 추가 설정 불필요.

만약 다른 결제 수단을 추가하고 싶다면:
- **토스 송금 링크**: 토스 앱 → 더보기 → 송금 링크 만들기
- **Buy Me a Coffee** (글로벌): buymeacoffee.com 가입
- **Lemon Squeezy** (한국 카드, 사업자등록 불필요): lemonsqueezy.com 가입

추가 결제 수단을 넣으려면 `index.html` 안의 후원 모달(`<div class="ov" id="supportOv">`)에 HTML 블록을 추가하세요.

---

## 🐙 Step 3. GitHub 저장소 생성

### 3-1. 저장소 만들기

1. [github.com](https://github.com)에서 우상단 "+" → "New repository"
2. Repository name: `nurse-duty-scheduler` (또는 본인이 원하는 이름)
3. Public 선택 (Vercel 무료 플랜에선 Private도 가능하지만 Public이 무난)
4. "Add a README" 체크 해제 (이미 우리가 만들어둠)
5. "Create repository" 클릭

### 3-2. 파일 업로드 (웹 방식 — 가장 쉬움)

1. 만들어진 저장소 페이지에서 "uploading an existing file" 클릭
2. 위 9개 파일을 모두 드래그 앤 드롭
3. 아래쪽 "Commit changes" 클릭

### 대안: 명령줄 사용

Git을 쓸 줄 아시면:
```bash
cd /path/to/your/files
git init
git add .
git commit -m "Initial release v3.9"
git branch -M main
git remote add origin https://github.com/USERNAME/nurse-duty-scheduler.git
git push -u origin main
```

---

## 🚀 Step 4. Vercel 배포

### 4-1. Vercel 가입 & 연동

1. [vercel.com](https://vercel.com)에서 "Sign Up" → "Continue with GitHub" 선택
2. GitHub 권한 승인

### 4-2. 프로젝트 생성

1. Vercel 대시보드에서 "Add New..." → "Project"
2. 본인 GitHub 저장소 목록에서 `nurse-duty-scheduler` 찾아 "Import"
3. 설정 화면:
   - **Framework Preset**: `Other` (그대로 두면 됨)
   - **Build Command**: 비워두기
   - **Output Directory**: 비워두기 (또는 `.`)
   - **Install Command**: 비워두기
4. "Deploy" 클릭

약 30초 후 배포 완료. `https://nurse-duty-scheduler.vercel.app` 같은 URL이 생성됩니다.

### 4-3. 동작 확인

생성된 URL을 클릭해서 다음 확인:
- [ ] 도구가 정상 로드되는지
- [ ] 좌상단 ⓘ 클릭 → About 모달 정상
- [ ] About 모달 안 💬 피드백 버튼 → 모달 정상 → 테스트 전송 → 본인 이메일로 도착하는지
- [ ] About 모달 안 💝 후원 버튼 → 모달 정상 → 링크 정상
- [ ] 휴대폰 크롬에서 접속 → 메뉴 → "홈 화면에 추가" 가능한지

---

## 🌐 Step 5. 커스텀 도메인 (선택)

`.vercel.app` 도메인도 무방하지만, 본인 도메인이 있으면 더 좋습니다.

### 도메인 구입

| 등록기관 | .kr | .com | .app |
|---|---|---|---|
| [가비아](https://gabia.com) | 1.5만 | 1.5만 | 2만 |
| [후이즈](https://whois.co.kr) | 1.5만 | 1.5만 | 2만 |
| [Cloudflare](https://cloudflare.com) | - | $11 | $14 |

추천 도메인 예시:
- `dutyscheduler.kr`
- `nurseduty.kr`
- `duty.app`

### Vercel에 도메인 연결

1. Vercel 프로젝트 → Settings → Domains
2. 도메인 입력 → "Add"
3. 표시되는 DNS 레코드를 도메인 등록기관에서 설정
4. 약 10분~수시간 후 자동 연결

---

## 📢 Step 6. 출시 (Soft Launch)

배포가 끝나면, **즉시 마케팅하지 마세요**. 다음 단계를 권장합니다.

### Week 1: Friends & Family Test (5~10명)
- 박 선생님 지인 간호사들에게 먼저 URL 공유
- 카카오톡으로 "테스트 해보고 피드백 부탁드려요" 한 마디
- 피드백 모이면 버그 수정

### Week 2~3: 카페·블라인드 한 군데씩

**좋은 후기 글 작성 팁:**
- 본인이 만들었다고 강조하지 말 것 (광고로 보임)
- "이런 도구를 발견했는데 써보니 좋더라" 톤
- 스크린샷 2~3장 첨부
- 작성 카페: "간호사 모여라" (네이버), "병원 간호사 카페" (다음) 등
- 블라인드: 간호사 라운지 게시판

### Week 4+: 본격 마케팅
- 인스타그램 계정 운영 (`@nurseduty_kr` 같은 핸들)
- 사용자 100명 넘으면 → 후원 채널 본격 안내

---

## 🛡️ Step 7. 운영 (정기 점검)

### 매주 확인
- Formspree 받은 피드백 확인
- Vercel Dashboard에서 트래픽 확인 (무료 플랜은 월 100GB까지)

### 매월 확인
- 후원 입금 확인
- 받은 피드백 종합 → 다음 버전 개발 우선순위 결정

### 새 버전 배포
1. `index.html` 수정
2. `service-worker.js`의 `CACHE_VERSION` 숫자 증가 (예: `v3.9.0` → `v3.10.0`)
   - 이걸 안 바꾸면 기존 사용자가 새 버전을 못 받습니다 (캐시 때문)
3. About 모달 안의 "Version 3.9 · Public Release" 숫자도 갱신
4. GitHub에 push → Vercel 자동 배포 (약 30초)

---

## ⚠️ 흔한 문제 해결

### "Service Worker 등록 실패" 에러
→ HTTPS가 아니면 SW가 동작 안 합니다. Vercel은 자동으로 HTTPS이므로 문제 없음. file:// 로컬 테스트에선 동작 안 함.

### 피드백 폼 전송 실패
→ Formspree 무료 플랜은 월 50건 한도. 초과 시 다음 달 1일에 리셋됨.
→ FORMSPREE_ENDPOINT가 잘못 교체된 경우. `index.html`을 다시 확인.

### 새 버전을 배포했는데 사용자한테 안 보임
→ Service Worker의 캐시 때문. `service-worker.js`의 `CACHE_VERSION`을 변경하지 않은 경우 발생.
→ 사용자에게 "강제 새로고침 (Ctrl+Shift+R 또는 ⌘+Shift+R)" 안내.

### PWA "홈 화면에 추가"가 안 보임
→ Safari (iOS)는 별도 "공유 → 홈 화면에 추가" 메뉴 사용
→ Chrome (Android)는 메뉴 → "앱 설치"
→ HTTPS여야 하고, manifest.json + 192px 아이콘이 정상 로드되어야 함

---

## 📞 추가 도움

기술적 막힘이 있으면 다음 채널을 참고:
- Vercel 공식 문서: vercel.com/docs
- Formspree 공식 문서: help.formspree.io
- GitHub 기본 가이드: docs.github.com/get-started

---

배포가 끝나면 박 선생님이 만드신 도구가 전 세계에서 접속 가능한 인터넷 서비스가 됩니다. 🎉
