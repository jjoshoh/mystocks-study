# 프로젝트: 내 포트폴리오 (미국주식 개인 투자 앱)

## 소유자 정보
- 사용자는 한국어 사용자이며, 한국 증권사에서 약 10년 브로커로 재직한 경력이 있는 미국주식 투자자다.
- 개발 지식은 깊지 않으므로 기술 용어는 쉽게 풀어서 설명하고, 명령 실행 전에 무엇을 하는지 한 줄로 알려줄 것.
- 대화는 항상 한국어로 한다.

## 프로젝트 개요
스마트폰에서 쓰는 개인 포트폴리오 관리 웹앱(PWA). Claude Cowork에서 v1을 만들었고,
이후 개발·배포는 Claude Code에서 이어간다.

- `index.html` — 모바일용 앱 (메인 산출물, 단일 파일, 외부 빌드 없음)
- `desktop.html` — 데스크톱용 대시보드 (참고용 이전 버전)

## 현재 상태 (2026-08-13 기준)
- 프로젝트/저장소 이름: `mystocks-study` (사용자 요청으로 my-portfolio에서 변경)
- 배포 완료: https://jjoshoh.github.io/mystocks-study/ (GitHub Pages, main 브랜치 루트)
- GitHub 저장소: https://github.com/jjoshoh/mystocks-study (public, gh CLI 로그인 계정: jjoshoh)
- 수정 후 main에 push하면 1~2분 내 폰 앱에 자동 반영됨
- 보유종목 8개: CRDO, SNDK, MU, BE, ALAB, AMD, CRWD, GOOG
- 시세는 2026-08-13 장중 스냅샷이 코드에 내장되어 있음 (`DEFAULTS` 배열)
- 수량·평단가는 localStorage에 저장 (`pf_holdings` 키)
- 실시간 시세: Finnhub API (사용자가 ⚙설정에서 키 입력 → `pf_apikey`에 저장)
- AI 종목분석: 카드의 "분석" 버튼 → Finnhub 데이터 리포트(52주 범위·재무지표·실적·뉴스)
  + Claude API 해설(선택, 키는 `pf_aikey`에 저장, 모델 claude-opus-5, 투자 추천 금지 프롬프트)
- 전략 백테스트: 메인 화면 "🧪 전략 백테스트" 버튼 → 단순 보유/이동평균 교차/RSI/매월 적립(DCA)
  4개 전략, 총수익률·CAGR·MDD·승률 + 자산 곡선 캔버스 차트. 과거 일봉은 Twelve Data API
  (사용자가 ⚙설정에서 무료 키 입력 → `pf_tdkey`에 저장, 액면분할 반영 adjust=splits)

## 로드맵 (사용자와 합의된 순서)
1. ~~포트폴리오 대시보드~~ (완료)
2. ~~AI 종목분석: 관심 종목의 재무·뉴스·기술적 지표를 종합한 분석 리포트 기능~~ (완료)
3. ~~전략 백테스팅: 매매 전략을 과거 데이터로 검증~~ (1차 완료 — 전략 4종, 클라이언트 계산)
- 참고 오픈소스: OpenBB, virattt/ai-hedge-fund, vectorbt, Ghostfolio

## 코드 규칙
- 단일 HTML 파일 유지 (CSS/JS 인라인, 빌드 도구 없음) — 사용자가 파일 하나로 관리하길 원함
- UI 언어는 한국어
- 색 규칙: 상승 = 빨강(--up), 하락 = 파랑(--down) — 한국식 표기, 바꾸지 말 것
- 색상 팔레트는 CSS 변수(--s1~--s8, --up, --down 등)로 정의되어 있음. 라이트/다크 모드 모두 지원 유지
- localStorage 접근은 반드시 try/catch 래퍼(store 객체)를 통해서만 — 미지원 환경에서 메모리로 대체됨
- 금액 표기: 달러, 소수 2자리, 천단위 콤마
- 투자 조언·매수매도 추천 기능은 넣지 않는다 (개인 기록·분석 도구로 유지)

## 주의
- Finnhub API 키는 코드에 하드코딩하지 말 것 (사용자별 설정으로 유지)
- 시세 스냅샷을 갱신할 때는 SNAPSHOT_TIME 상수도 함께 갱신
