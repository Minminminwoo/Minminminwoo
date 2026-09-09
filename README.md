## PlayUs — 야구 직관 기록 공유 커뮤니티

**[KEA-ChunSam](https://github.com/KEA-ChunSam)** · 카카오 엔터프라이즈 아카데미 6기 3팀 · 2025.03 ~ 2025.07
팀 8명 (BE 4 / FE 2 / Infra 1 / AI 1) · **Back-End Lead**

KBO 팬을 대상으로 직관 모임(직관팟) 모집, 실시간 채팅, 커뮤니티, 직관일지, AI 경기 시뮬레이션을 제공하는 MSA 기반 플랫폼입니다.
[조직 레포 전체 보기](https://github.com/orgs/KEA-ChunSam/repositories)

<p>
  <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=Spring-Boot&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=Spring-Security&logoColor=white"/>
  <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON-Web-Tokens&logoColor=white"/>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white"/>
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=MongoDB&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-FF4438?style=for-the-badge&logo=Redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white"/>
</p>

### 담당 — [PlayUs-user-service](https://github.com/KEA-ChunSam/PlayUs-user-service)

회원/인증 도메인 전담. 전체 인터페이스 명세서 68개 API 중 23개를 설계·구현했습니다.

- **MSA 환경 인증/인가 시스템**
  Cookie + JWT 기반. Access Token 6시간 / Refresh Token 7일로 분리하고, Refresh Token은 Redis에 TTL을 만료시각과 동일하게 두어 저장합니다. user-service에서 발급한 쿠키를 다른 서비스에서도 사용할 수 있도록 구성했습니다.
- **OAuth 로그인**
  Kakao / Naver 소셜 로그인, 토큰 재발급, 로그아웃 시 토큰 블랙리스트 처리
- **유저 도메인 API**
  회원가입, 선호팀 등록/수정, 닉네임 변경, 회원 탈퇴, 프로필 조회(상세/간단/타 유저), 유저 태그 평가 등록 및 요약 조회
- **알림 API**
  직관팟·댓글 알림 생성, 알림 내역 조회, SSE 구독 엔드포인트
- **타 MSA 호출용 내부 API**
  토큰 블랙리스트 검증, 직관팟 작성자·참여자·지원자 정보 조회
- **공통 기반 작업**
  MySQL entity·enum 초기 설계, MySQL·MongoDB Soft Delete 적용, MSA 간 호출 시 CQRS Config 내부 필터 분기 처리, 이미지 업로드용 Presigned URL 발급

### 설계 및 검증

- **ERD 및 DB 설계 참여**
  테이블 명세서 18개, 예외 정책 44건 정리에 참여
- **테스트 시나리오 16건 중 13건 작성, 8건 직접 수행 및 리뷰**
  요구사항에서 기대값을 먼저 정의한 뒤 구현하는 순서로 진행했습니다.
- **Presigned URL 기반 이미지 업로드**
  업로드 트래픽을 애플리케이션 서버에서 분리하고, 서버는 URL 저장만 담당하도록 했습니다.

### 팀 성과

- k6 기반 단계적 부하 테스트(동시 사용자 500 → 10,000)에서 누적 120만 건 이상 요청 처리, 초당 1,353건, 정상 요청 평균 응답 93ms
- Kafka + Debezium CDC 파이프라인으로 MySQL → MongoDB / Elasticsearch 실시간 동기화 및 Read/Write 분산
- Kubernetes + ArgoCD GitOps 배포, Terraform IaC, LGTM 스택 기반 모니터링
- PR 기반 코드 리뷰에 CodeRabbit 도입. 테스트 전량 통과 및 최소 1인 승인 시에만 merge 가능하도록 브랜치 룰 운영

<br>

## DK테크인 PBL — 사내 지식 관리 플랫폼 & RAG 챗봇

**dktechin-pbl** · 2025.07 ~ 2025.08 · 팀 11명 (PM 1 / FE 2 / BE 6 / AI 2) · **Back-End**

> 기업 협업 프로젝트로, **소스코드와 상세 설계는 비밀유지 조항에 따라 비공개**입니다.

<p>
  <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=Spring-Boot&logoColor=white"/>
  <img src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logoColor=white"/>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white"/>
  <img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=Elasticsearch&logoColor=white"/>
</p>

### 담당

- **조직 / 부서 / 권한 도메인 API 11종**
  대시보드 조회, 히스토리 조회·필터, 부서 생성·수정·삭제, 관리자 초대·부서 변경·설정 조회
- **이메일 기반 관리자 초대 및 권한 부여·박탈 로직** 설계 및 구현
- **메신저 연동 챗봇과 AI 모델 간 소켓 통신** 클라이언트 측 구현
- **관리자 페이지 백엔드** 전반 구현

### 산출물 및 검증

- ERD, 테이블 명세서, API 명세서, 기능 명세서 작성
- 도메인별 표준 에러 코드 기반 에러 테스트 명세서 작성
- JaCoCo 테스트 커버리지 리포트 관리(전체 51%)

### 협업

- WBS · 요구사항 명세 · 테스트 시나리오 산출물 관리, CodeRabbit 기반 PR 코드 리뷰
- 기본 요구사항 전량 충족 + 추가 기능 10건 중 8건 구현(팀 결과)

<br>
