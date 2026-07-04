# 🌊 OceanKeeper (바다살리기네트워크)

> 해양 정화 봉사활동을 연결하고, 수거 기록·통계·커뮤니티를 한 곳에서 관리하는 웹 플랫폼
>
> **🔗 Live: [oceankeeper.org](https://oceankeeper.org)** · 팀 프로젝트 (5인) · 배포 운영 중

---

## 📖 소개

**OceanKeeper**는 해변·해양 정화 자원봉사 단체와 참여자를 연결하는 서비스입니다.
봉사 일정 모집부터 현장 수거 기록, 활동 통계 시각화, 참여자 커뮤니티까지
봉사 활동의 전 과정을 하나의 플랫폼에서 관리할 수 있도록 만들었습니다.

현재 **[oceankeeper.org](https://oceankeeper.org)** 로 실제 배포·운영 중입니다.

## 🙋 내 역할 (Full-stack)

5인 팀에서 **프론트엔드 · 백엔드를 함께 담당**했습니다. (FE ~56 커밋 / BE ~36 커밋)

### 🔧 대표 트러블슈팅 — 낙관적 업로드 + 비동기 압축 파이프라인 (설계 제안)
- **문제:** 이미지 업로드 시 압축을 **동기**로 처리하면 **6~7초간 사용자가 결과를 못 보고 대기**해야 했다. 프론트(클라이언트) CPU 압축은 저사양 기기에서 느리고 버벅였다.
- **설계(낙관적 업로드):**
  1. **원본을 압축 없이 즉시 업로드** → 사용자는 곧바로 이미지 확인 (대기 제거)
  2. **Azure Functions가 백그라운드에서 비동기 압축·리사이징(WebP)**
  3. 압축본이 올라오면 **DB의 이미지 경로를 압축본으로 교체(swap)**
  4. 원본은 **cold 스토리지로 이동** → 저장 비용 절감
- **효과:** 이미지 처리 체감 **6~7초 → 0.2~0.3초**, 이미지 용량 **2.6MB → 344KB (~8배↓)**.

### 주요 기여
- **인증 / 권한 (BE 주도)** — 참여자 / 기록자(RECORDER) / 관리자 3단계 역할. Spring Security + JWT(Stateless)로 API 레벨 접근 제어, NextAuth 세션과 연동
- **커뮤니티 & 마이페이지** — 후기 작성/수정/삭제, 내 작성글·대기글 관리, 활동 기록과 임시저장 명확화 (JPA 도메인 설계, N+1은 fetch join으로 최소화)
- **통계 시각화** — 기간·단체·지역별 수거량 추이·품목별 분포를 Nivo/ECharts 대시보드로 (집계 JPQL + 시각화)
- **수거 기록 통합** — 봉사 수거 기록을 커뮤니티 후기 수정 플로우에 통합하고 재사용 로직으로 정리
- **모바일 / PWA** — 반응형 이슈 해결, `next-pwa` + Dexie(IndexedDB) 오프라인 캐시, 공유 기능

> 팀 저장소는 조직 소유의 비공개 레포입니다. 이 저장소는 프로젝트 소개·역할 정리를 위한 포트폴리오 페이지이며, 실제 소스 코드는 포함하지 않습니다.

## 🛠 기술 스택

**Frontend**
- Next.js 16 (App Router, SSR) · React · TypeScript
- NextAuth.js (인증/세션) · React Hook Form
- Radix UI · Tailwind CSS · Nivo / ECharts (통계 시각화)
- PWA (`next-pwa`) · Dexie (IndexedDB 오프라인 캐시) · Axios

**Backend**
- Spring Boot 3.5 · Java 17 · Maven
- Spring Data JPA · Spring Security · JWT (jjwt)
- PostgreSQL · Spring AOP · Actuator
- **Azure Functions** (서버리스 비동기 이미지 압축)
- Azure Blob Storage (hot/cold 계층 저장) · Thumbnailator / WebP (이미지 최적화)

**Infra / 운영**
- 도메인 배포: oceankeeper.org
- `release` / `dev` 브랜치 운영, dev 개발 서버 분리

## ✨ 주요 기능

| 영역 | 내용 |
|------|------|
| 봉사 모집 | 단체별 봉사 일정 등록·신청 |
| 수거 기록 | 현장 폐기물 수거량·사진 기록, 임시저장 |
| 통계 | 활동/수거 데이터 차트 시각화 |
| 커뮤니티 | 후기·공지 게시판, 다중 이미지 업로드 |
| 권한 관리 | 참여자 / 기록자(RECORDER) / 관리자 역할 분리 |
| 마이페이지 | 내 활동·작성글 관리 |

## 📸 스크린샷

> _실제 배포 사이트 **[oceankeeper.org](https://oceankeeper.org)** 화면 (2026-07 기준)_

### 메인 (데스크톱)

![메인 랜딩 — 히어로, 주요 기능 안내, 누적 활동 지표, 협력 단체](docs/screenshots/desktop-landing.png)

*랜딩 페이지 — 서비스 소개 히어로, 4대 핵심 기능, 누적 수거량·활동·참여자 지표, 협력 단체 로고.*

### 해양 쓰레기 지도 (데스크톱)

![해양 쓰레기 수거 활동 지도 — 전국 활동 위치와 활동 목록](docs/screenshots/desktop-map.png)

*활동 지도 — 전국 정화 활동 위치를 지도에 시각화하고, 좌측에서 활동 목록·필터를 제공.*

### 데이터 통계 (데스크톱)

![데이터 통계 대시보드 — 수거량 추이, 품목별 분포, 참여 인원 차트](docs/screenshots/desktop-statistics.png)

*통계 대시보드 — 기간·단체·지역별 수거량 추이, 품목별 분포(도넛), 활동/참여 인원 추이를 차트로 시각화.*

### 메인 (모바일)

<img src="docs/screenshots/mobile-landing.png" alt="모바일 반응형 랜딩 화면" width="320" />

*모바일 반응형 — 좁은 화면에 맞춰 재배치되는 랜딩 화면 (PWA 지원).*

---

<sub>본 저장소는 개인 포트폴리오/이력서 용도의 프로젝트 소개 페이지입니다.</sub>
