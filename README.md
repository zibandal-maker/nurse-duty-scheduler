# Nurse Duty Scheduler

> 한국 간호 표준에 부합하는 무료 간호사 3교대 듀티 자동 배치 도구

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 주요 기능

- ✅ **자동 듀티 배치**: 가중치 기반 알고리듬, 선임-신규 비율 자동 조정
- ✅ **금지 패턴 검사**: NOD, EOD, ED, ND, NE, NON, NOE, NNNN — 한국 간호 표준
- ✅ **간호사 속성**: 임산부 / 야간전담 / 야간면제 / 고정근무 / 프리셉터 페어
- ✅ **원티드 듀티 관리**: 사전 신청 → 락 → 자동배치 시 보존
- ✅ **충돌 검사**: 실시간 위반 패널, 셀별 시각 표시
- ✅ **Excel 출력**: 인쇄용 듀티표 + 통계 리포트
- ✅ **PWA**: 홈 화면 추가 → 앱처럼 실행, 오프라인 지원
- ✅ **개인정보 0**: 모든 데이터는 사용자 브라우저(localStorage)에만 저장

## 사용

웹 브라우저에서 [URL]로 접속하세요. 별도 설치 불필요.

모바일/태블릿에서 "홈 화면에 추가"를 누르면 앱처럼 사용 가능합니다.

## 파일 구성

```
index.html         메인 도구 (단일 HTML, ~220KB)
manifest.json      PWA 메타데이터
service-worker.js  오프라인 캐싱
icon-192.png       PWA 아이콘 (192x192)
icon-512.png       PWA 아이콘 (512x512)
```

## 배포 (Vercel)

### 1. GitHub 저장소 만들기

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/USERNAME/nurse-duty-scheduler.git
git push -u origin main
```

### 2. Vercel 연결

1. [vercel.com](https://vercel.com)에서 GitHub 계정으로 로그인
2. "New Project" → 위 저장소 선택
3. Framework Preset: **Other** (정적 사이트라 빌드 설정 없음)
4. "Deploy" 클릭 → 약 30초 후 배포 완료

배포되면 `https://your-project.vercel.app` 같은 URL이 생성됩니다.

### 3. 커스텀 도메인 (선택)

Vercel Dashboard → Project → Settings → Domains에서 도메인 연결.
한국 도메인은 가비아·후이즈에서 `.kr` 1.5만원/년 정도.

## 배포 전 체크리스트

배포 전 `index.html` 안의 **플레이스홀더**를 본인 정보로 교체해야 합니다.

### Formspree 엔드포인트 (피드백 수집)

1. [formspree.io](https://formspree.io) 가입 (무료 월 50건)
2. New Form 생성 → 본인 이메일 등록
3. 받은 엔드포인트 URL을 `index.html`의 다음 라인에서 교체:

```js
var FORMSPREE_ENDPOINT = 'https://formspree.io/f/REPLACE_WITH_YOUR_FORM_ID';
```

### 후원 링크

`index.html` 안의 후원 모달에서 다음 플레이스홀더를 본인 URL로 교체:

- `https://www.buymeacoffee.com/_____` → Buy Me a Coffee 본인 페이지
- `https://_____.lemonsqueezy.com/` → Lemon Squeezy 상품 URL
- `https://toss.me/_____` → 토스 송금 링크 (toss.me 가입 후 발급)
- `https://qr.kakaopay.com/_____` → 카카오페이 QR 결제 링크

각 서비스 가입 방법:
- **Buy Me a Coffee**: buymeacoffee.com에서 가입, 무료, 글로벌 결제
- **Lemon Squeezy**: lemonsqueezy.com에서 가입, 사업자등록 불필요, 한국 카드 지원, 수수료 5%
- **토스 송금 링크**: toss 앱 → 더보기 → 송금 링크 만들기
- **카카오페이**: 카카오페이 앱 → QR결제 → 송금받기

## 라이선스

MIT License. 상업적 이용·수정·재배포 자유.

본 도구는 데모·실험 목적으로 제공됩니다. 실제 의료 현장에서의 안전성·정확성·법적 요건 충족 여부는 검증되지 않았으며, 사용으로 인한 결과에 대해 제작자는 어떠한 책임도 지지 않습니다.

## 기여

피드백·버그 신고는 도구 안의 💬 피드백 버튼을 이용해주세요.
