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

- **커뮤니티 & 마이페이지** — 후기 작성/수정/삭제, 내 작성글·대기글 관리, 활동 기록과 임시저장 명확화
- **수거 기록 통합** — 봉사 수거 기록을 커뮤니티 후기 수정 플로우에 통합하고 재사용 로직으로 정리
- **이미지 처리 공용화** — 다중 이미지 업로드 크기 문제 해결, 클라이언트 리사이징 유틸(`image-utils`) 추출·적용
- **인증/권한 UX** — 권한별 라우팅·회원가입·관리자 UI 버그 수정
- **모바일 대응** — 사이드바 자동 활성화 등 반응형 이슈 해결
- **공유 기능** 구현

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
- Azure Blob Storage (이미지 저장) · Thumbnailator / WebP (이미지 최적화)

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

> _배포 사이트에서 확인: **[oceankeeper.org](https://oceankeeper.org)**_
> _(스크린샷 이미지를 이곳에 추가할 수 있습니다)_

---

<sub>본 저장소는 개인 포트폴리오/이력서 용도의 프로젝트 소개 페이지입니다.</sub>
