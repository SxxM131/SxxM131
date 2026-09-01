# 프로젝트 정리

> 실생활의 불편함에서 출발해, AI와 웹 기술로 직접 해결책을 만들어 본 프로젝트 모음입니다.

---

## 목차

1. [MED](#1-med) — 복약 안전성 확인
2. [StocKKnock](#2-stockknock) — AI 주식 분석
3. [SVS Reservation (WOS1234)](#3-svs-reservation-wos1234) — 예약·배정 시스템
4. [Hexa](#4-hexa) — 허밍 기반 악보 거래
5. [Drafty](#5-drafty) — AI 글쓰기 Chrome Extension
6. [HotelBooker](#6-hotelbooker) — 호텔 예약 시스템
7. [Re:Cord](#7-record) — 공연 티켓 기록 앱
8. [AI SNS (나노바나나 프로)](#8-ai-sns-나노바나나-프로) — AI 콘텐츠 계정 운영

---

## 1. MED

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 배포 완료 |
| **역할** | 기획 · 풀스택 개발 (1인) |
| **GitHub** | [github.com/SxxM131/med](https://github.com/SxxM131/med) |

### 한 줄 소개

약물 알러지와 복용 경험을 기반으로, 안전한 약물을 추천하고 분석해 주는 개인 맞춤형 복약 안전성 확인 웹 서비스.

### 시작 계기

동생이 특정 항생제 성분에 알레르기가 있어, 약을 복용할 때마다 성분표를 일일이 확인해야 하는 불편함을 직접 겪었습니다. "약 성분을 촬영하면 알레르기 유발 성분을 자동으로 분석해 주는 서비스가 있으면 좋겠다"는 생각에서 출발했습니다.

### 주요 기능

- **사용자 인증** — 회원가입·로그인, JWT 인증, 닉네임·비밀번호 변경, 이메일 아이디 찾기
- **알러지 관리** — 약물·식품 알러지 등록 (7개 식품 카테고리, 심각도 설정), 모든 분석에서 자동 참조
- **증상 분석** — 현재 증상 입력 → GPT 기반 안전한 약 추천, 주의 약물·위험 요소 요약
- **부작용 분석** — 과거 부작용 약물 입력 → 공통 성분·민감 성분 분석, 부형제 위험도 평가
- **약 성분표 OCR** — 촬영한 성분표 인식 → AI 알레르기 성분 분석 → 대체 약 추천

### 기술 스택

| 영역 | 기술 |
|------|------|
| Frontend | React, Vite, TypeScript, Tailwind CSS |
| Backend | Spring Boot 3.3.5 (Java 17), REST API |
| 분석 서비스 | Python FastAPI |
| Database | PostgreSQL (로컬 / Supabase) |
| 인증 | JWT |
| AI | GPT-4o-mini, OCR |

### 시스템 구조

```
React (FE) ──HTTP/REST──▶ Spring Boot (BE) ──▶ PostgreSQL
                              │
                              └──▶ Python FastAPI (분석)
```

### 배운 점

- 가족의 실제 불편함에서 출발한 프로젝트라 사용자 관점 설계에 집중할 수 있었음
- 약사·의사 조언·병원 홍보 기능까지 기획했으나, 사용자 확보와 수익 구조 설계에서 한계를 경험
- **기술적으로 가능해도 서비스가 지속되려면 사용자·비즈니스 설계가 함께 필요**하다는 것을 배움
- JWT 인증을 직접 구현하며, Refresh Token·권한 분리까지는 더 보완이 필요하다고 느낌

---

## 2. StocKKnock

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 개발 중 |
| **역할** | 기획 · 풀스택 개발 (1인) |
| **GitHub** | [github.com/SxxM131/stockknock](https://github.com/SxxM131/stockknock) |

### 한 줄 소개

국내·해외 주식 투자자를 위한 AI 기반 통합 주식 분석 플랫폼. 실시간 시세, AI 시장 브리핑, 포트폴리오 관리, 가격 알림을 한곳에서 제공.

### 주요 기능

- **실시간 주가** — Yahoo Finance, Alpha Vantage, Twelve Data API 연동, 시장 개장 시간(평일 09:00–15:30)에만 1분마다 자동 갱신
- **오늘의 시장 브리핑** — GPT 기반 일일 시장 요약 (평일 1회 생성, DB 캐시)
- **유튜버 시장 브리핑** — 화이트리스트 채널 신규 영상 수집 → GPT 요약 (핵심 전망 / 언급 종목 / 투자 톤), 하루 2회 스케줄
- **포트폴리오 관리** — 보유 종목 관리, 실시간 손익 계산, AI 포트폴리오 종합 분석 (해시 기반 캐싱으로 불필요한 GPT 호출 방지)
- **가격 알림** — 목표가·손절가·변동률 기준 알림, 30초마다 조건 체크
- **AI 채팅** — 문맥 유지 대화형 AI 애널리스트, 최근 5개 대화 기반
- **뉴스 피드** — 최근 7일 뉴스 조회, 종목별 연관 뉴스 필터링, 뉴스·유튜버 브리핑 탭 전환
- **관심 종목** — 사용자별 관심 종목 추가·삭제

### 기술 스택

| 영역 | 기술 |
|------|------|
| Backend | Python |
| AI | OpenAI GPT (gpt-4o-mini) |
| 외부 API | Yahoo Finance, Alpha Vantage, Twelve Data, YouTube Data API v3 |
| 데이터 | 뉴스 크롤링, DB 캐시 |
| 스케줄링 | 시장 개장 시간 기반 자동 갱신 |

### 진행 상황 · 다음 단계

- YouTube API 연동 고도화
- 포트폴리오·가격 알림 기능 보완
- Phase 2: 사용자별 유튜브 채널 구독 (미구현)

### 배운 점

- 여러 외부 API를 하나의 서비스에 조합할 때 **장애 격리·재시도 로직**이 필수
- API 호출 비용 절감을 위해 **시장 개장 시간에만 갱신**, **DB 캐시**, **해시 기반 재분석 방지** 등 비용 최적화 설계 경험
- 외부 주가 API 호출 실패·응답 지연을 반복적으로 겪으며 Redis 캐싱의 필요성을 체감

---

## 3. SVS Reservation (WOS1234)

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 배포 완료 (Vercel) |
| **역할** | 기획 · 풀스택 개발 (1인) |
| **GitHub** | [github.com/SxxM131/wos1234](https://github.com/SxxM131/wos1234) |

### 한 줄 소개

취미 게임 커뮤니티(연맹)의 SVS(관직) 스케줄을 관리하고, 공정하게 예약·배정하는 모바일 퍼스트 웹앱.

> 원래 게임 클랜 스케줄 관리 웹사이트로 시작했으며, 이후 연맹 SVS 예약·배정 시스템으로 발전.

### 주요 기능

- **예약 제출** — 연맹원이 희망 시간대·관직을 선택해 예약 신청
- **자동 배정** — **Min-Cost Max-Flow** 알고리즘으로 공정한 예약 배정
- **예약 수정** — 제출 후 수정·취소 시나리오별 처리
- **관리자 페이지** — 비밀 URL 기반 관리, 배정 결과 확인·수정
- **Google Forms 연동** — (선택) 구글 폼과 연동해 예약 수집
- **모바일 퍼스트 UI** — 연맹원이 주로 모바일로 접속하는 환경에 맞춘 설계

### 기술 스택

| 영역 | 기술 |
|------|------|
| Frontend | Next.js 14, TypeScript |
| Backend / DB | Supabase (PostgreSQL) |
| 인증 | Iron Session |
| 배포 | Vercel |
| 알고리즘 | Min-Cost Max-Flow (예약 배정) |

### 배운 점

- 최적화 알고리즘을 실제 서비스에 적용하려면 **동시 예약·취소 같은 예외 케이스**까지 고려한 설계가 필요
- Supabase + Vercel 조합으로 빠르게 배포·운영 가능
- 운영 시나리오(예약 수정, 관리자 개입)를 미리 정의해 두는 것이 중요

---

## 4. Hexa

| 항목 | 내용 |
|------|------|
| **유형** | 팀 프로젝트 |
| **상태** | 배포 완료 |
| **역할** | 백엔드 (+ AI 기반 프론트엔드 병행) |
| **수상** | 해커톤 3등 |

### 한 줄 소개

흥얼거림을 음표로 바꾸고, AI로 보정·편곡한 뒤 악보를 사고파는 웹 플랫폼.

### 서비스 흐름

```
허밍 녹음 → 음표 추출 (Basic Pitch) → AI 음정 보정 (GPT)
    → 악보화 → 장르 선택 시 GPT 화음 편곡 → 완성곡 거래
```

### 주요 기능

- **허밍 → 음표 변환** — Spotify Basic Pitch로 오디오를 MIDI/음표로 변환
- **AI 음정 보정** — GPT로 음정 오차 보정 및 짧은 멜로디 생성
- **화음 편곡** — 장르 선택 시 GPT가 화음 편곡
- **악보 거래** — 완성된 악보·곡을 사고파는 마켓플레이스

### 기술 스택

| 영역 | 기술 |
|------|------|
| Frontend | TypeScript, JavaScript, CSS |
| Backend | (팀 내 백엔드 담당) |
| AI / 오디오 | Spotify Basic Pitch, GPT |
| 기타 | 거래 시스템 |

### 배운 점

- 오디오 처리와 AI 보정을 **하나의 파이프라인**으로 연결하는 경험
- 음정 보정처럼 정답이 명확하지 않은 문제일수록 **사람이 기준값을 정해줘야** AI 결과를 신뢰할 수 있음
- 디자인팀 Figma 설계를 Cursor로 연동해 프론트엔드까지 구현

---

## 5. Drafty

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 배포 완료 · Chrome Web Store 등록 · 실사용자 보유 |
| **역할** | 기획 · 개발 · 배포 전 과정 (1인) |
| **GitHub** | [github.com/SxxM131/drafty](https://github.com/SxxM131/drafty) |

### 한 줄 소개

웹페이지 요약과 이메일·문장 교정을 제공하는 AI 글쓰기 Chrome Extension. 미국·홍콩 등 해외 실사용자 확보.

### 시작 계기

외국 교수님께 예의를 갖춘 영어 이메일을 쓰기 어렵다는 문제를 느꼈습니다. 짧은 글을 원하는 톤으로 다듬거나, 긴 글을 요약해 주는 도구가 필요했습니다.

### 주요 기능

**Enhance (AI Writer)**
- 입력 필드(이메일, 채팅, 문서)에서 텍스트 선택 후 **Enhance** 클릭
- 5가지 톤: Neutral, Professional, Casual, Witty, Concise
- 문맥 인식 기반 문법·명확성·흐름 개선

**Extract (AI Summarizer)**
- 웹페이지 텍스트 선택 후 **Extract** 클릭
- 불릿 포인트 요약, 드래그 가능한 플로팅 카드 UI
- 복사, 글꼴 크기 조절, 재시도 기능

**기타**
- 다크 모드 (시스템 테마 자동 적용)
- 툴바에서 톤 설정
- iOS 키보드 앱 (Beta) — 이동 중에도 문장 다듬기

### 기술 스택

| 영역 | 기술 |
|------|------|
| Extension | Chrome Extension Manifest V3, Vanilla JS, HTML, CSS |
| Backend | Node.js, Express, OpenAI API (GPT-4o / GPT-3.5-turbo) |
| 배포 | Render (Web Service) |
| iOS (Beta) | Swift, Xcode |

### 운영 경험

- Chrome Web Store 출시 후 **미국, 홍콩** 등 해외 실사용자 확보
- 사용자 증가에 따라 **OpenAI API 호출 비용**이 함께 늘어, 결국 제 사비로 운영비 감당
- HTTPS로 텍스트 전송, 처리 후 즉시 폐기 (개인정보 미저장)

### 배운 점

- **기획 → 개발 → 스토어 등록 → 실사용자**까지 1인으로 완주한 경험
- 소규모 서비스라도 실사용자가 있으면 **API 비용·트래픽 모니터링**이 필수
- 캐싱·비용 최적화 없이는 서비스를 안정적으로 유지하기 어렵다는 것을 체감

---

## 6. HotelBooker

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 개발 완료 |
| **역할** | 풀스택 개발 (1인) |
| **GitHub** | [github.com/SxxM131/HotelBooker](https://github.com/SxxM131/HotelBooker) |

### 한 줄 소개

복잡한 DB 설계·관리 연습을 목적으로 만든 호텔 객실 예약 시스템. 사용자 예약부터 관리자 대시보드, 결제, 리뷰까지 호텔 운영에 필요한 기능을 포함.

### 주요 기능

**사용자**
- 회원가입·로그인 (JWT), 아이디/비밀번호 찾기 (이메일 인증)
- 객실 조회 (목록, 상세, 이미지), 예약·조회·취소
- 결제 (카드, 계좌이체, 현금), 리뷰·평점 작성
- 마이페이지 (예약 내역, 리뷰 관리), 공지사항

**관리자**
- 대시보드 (예약·체크인·체크아웃 현황, 객실 상태, 월별 매출)
- 객실 CRUD, 예약 상태 변경, 리뷰 공개/비공개·관리자 답변
- 공지사항 관리, 기간별 통계·매출 분석

### 기술 스택

| 영역 | 기술 |
|------|------|
| Backend | Spring Boot 3.3.4, Java 17, Spring Data JPA, Spring Security + JWT |
| Frontend | React 19, Vite 7, Tailwind CSS, React Router, Axios |
| Database | PostgreSQL |
| API 문서 | SpringDoc OpenAPI (Swagger) |
| 이메일 | Spring Mail (Gmail SMTP) |

### 배운 점

- 예약·결제·리뷰·관리자 권한이 얽힌 **복잡한 DB 스키마** 설계 경험
- 사용자/관리자 역할 분리, JWT 기반 인증·인가 구현
- Swagger로 API 문서화하여 프론트·백엔드 연동 효율화

---

## 7. Re:Cord

| 항목 | 내용 |
|------|------|
| **유형** | 팀 프로젝트 (학교 졸업 프로젝트, 1년) |
| **상태** | 개발 완료 |
| **역할** | 기획 · 백엔드 |
| **GitHub** | [github.com/SxxM131/ReMade](https://github.com/SxxM131/ReMade) |

### 한 줄 소개

관람한 공연을 티켓 형식으로 기록하고, OCR·STT·AI 이미지 생성으로 후기를 남기는 풀스택 앱. 친구 추가·티켓 공유 등 SNS 기능 포함.

### 주요 기능

- **티켓 기록** — 공연 관람 내역을 티켓 형식으로 저장·관리
- **OCR** — 티켓 사진에서 공연명·날짜·좌석 정보 자동 추출 (Google Cloud Vision)
- **STT** — 공연 후기를 음성으로 녹음 → 텍스트 변환 (Google STT → Whisper 교체)
- **이미지 생성** — DALL-E 3로 티켓 이미지 생성 (정책 변경 시 Stable Diffusion 대체)
- **GPT 다듬기** — 후기 텍스트 AI 교정
- **SNS** — 친구 추가, 티켓 공유
- **파일 저장** — AWS S3

### 기술 스택

| 영역 | 기술 |
|------|------|
| Backend | Java, Spring Boot, PostgreSQL, JWT |
| Frontend | React Native (iOS 포함) |
| AI | OCR (Google), STT (Whisper), DALL-E 3, Stable Diffusion, GPT |
| Storage | AWS S3 |
| 인증 | 이메일 인증 (Spring Mail) |

### 기술적 어려움과 해결

**1. DALL-E 정책 변경**
- 개발 막바지 DALL-E 3 정책 변경으로 며칠간 이미지 생성 중단
- Stable Diffusion으로 전체 로직 교체 → 이후 DALL-E 정상화로 원복하는 시행착오
- → **외부 API 의존 시 대체 옵션을 미리 준비**해야 함

**2. STT API 제약**
- Google STT가 **1분 단위로만 인식**된다는 제약을 개발 완료 후 발견
- 1분 분할 vs Whisper 전체 교체 검토 → **Whisper로 교체**
- → **외부 API는 개발 초반에 제약 조건부터 테스트**해야 함

**3. 멀티 API 통합**
- OCR, STT, 이미지 생성 API마다 응답 형식·에러·비용 구조가 다름
- API별 타임아웃·재시도·폴백 로직 분리, 한 API 장애가 전체를 멈추지 않도록 설계

### 협업 경험

- 1년 단위 졸업 프로젝트로 팀원 간 일정·작업 방식 차이 경험
- 구체적 일정·역할 분담, 2시간 이내 답장, 매주 진행 공유 회의 규칙으로 해결
- → 연락 두절, 방향성 차이, 주제 변경 등 갈등 대응 방법 습득

### 배운 점

- **가장 열정을 갖고 진행한 프로젝트** — 공연 기록 경험 자체가 동기
- 외부 AI API 3종 통합, 정책 변경·호출 제약·대체 수단 준비의 중요성
- 단순 CRUD를 넘어 멀티모달(OCR·STT·이미지)을 하나의 서비스로 엮는 경험

---

## 8. AI SNS (나노바나나 프로)

| 항목 | 내용 |
|------|------|
| **유형** | 개인 프로젝트 |
| **상태** | 종료 |
| **역할** | 기획 · 콘텐츠 제작 · 계정 운영 (1인) |

### 한 줄 소개

고양이 3마리가 세계여행을 떠나는 컨셉의 AI 콘텐츠 SNS 계정 운영. 이미지·영상·ASMR 콘텐츠를 생성형 AI로 제작.

### 콘텐츠 컨셉

- **캐릭터** — 3마리 고양이의 세계여행 스토리
- **콘텐츠 유형** — AI 이미지, 영상, ASMR
- **핵심 과제** — 캐릭터·세계관 **일관성 유지** (프롬프트 엔지니어링, 스타일 가이드)

### 사용 도구

| 도구 | 용도 |
|------|------|
| 나노바나나 프로 | 이미지 생성 |
| Sora | 영상 생성 |
| Kling AI | 영상 생성 |
| 기타 멀티모달 AI | ASMR, 이미지·영상 보조 |

### 관련 프로젝트

- **[clips](https://github.com/SxxM131/clips)** — 영상 병합, AI 프롬프트 생성(asrm/meow), YouTube 클립 자동 추출 웹 도구. AI SNS 콘텐츠 제작 파이프라인의 일부로 활용.

### 종료 배경

- 생성형 AI 콘텐츠에 대한 **사회적 시선 변화**를 겪으며 운영 종료
- 캐릭터 일관성 유지, AI 도구 업데이트 대응, 콘텐츠 제작 비용·시간 등 지속 운영의 한계

### 배운 점

- 생성형 AI로 **스토리텔링 콘텐츠**를 만드는 전 과정 (기획 → 프롬프트 → 생성 → 편집 → 게시)
- 캐릭터 일관성은 프롬프트 설계·참조 이미지·스타일 가이드가 핵심
- AI 콘텐츠의 사회적 수용도·윤리적 이슈에 대한 고민

---

## 프로젝트 한눈에 보기

| # | 프로젝트 | 유형 | 상태 | 역할 | 핵심 기술 |
|---|----------|------|------|------|-----------|
| 1 | MED | 개인 | 배포 완료 | 1인 풀스택 | Spring Boot, React, GPT, OCR |
| 2 | StocKKnock | 개인 | 개발 중 | 1인 풀스택 | Python, GPT, 뉴스 크롤링, YouTube API |
| 3 | SVS Reservation | 개인 | 배포 완료 | 1인 풀스택 | Next.js, Supabase, Min-Cost Max-Flow |
| 4 | Hexa | 팀 | 배포 완료 | 백엔드 | Basic Pitch, GPT, 해커톤 3등 |
| 5 | Drafty | 개인 | 스토어 출시 | 1인 전 과정 | Chrome Extension, OpenAI, 해외 실사용자 |
| 6 | HotelBooker | 개인 | 개발 완료 | 1인 풀스택 | Spring Boot, React, PostgreSQL |
| 7 | Re:Cord | 팀 | 졸업 프로젝트 | 기획·백엔드 | OCR, STT, DALL-E, Whisper, Spring Boot |
| 8 | AI SNS | 개인 | 종료 | 1인 운영 | 나노바나나, Sora, Kling AI |

---

## 기술 스택 요약

| 분야 | 사용 기술 |
|------|-----------|
| **Language** | Java, Python, TypeScript, JavaScript |
| **Frontend** | React, Next.js, Vite, Tailwind CSS, React Native |
| **Backend** | Spring Boot, FastAPI, Node.js, Express |
| **Database** | PostgreSQL, Supabase |
| **AI / ML** | GPT, DALL-E, Whisper, OCR, STT, Basic Pitch, Stable Diffusion |
| **Infra** | Vercel, Render, AWS S3, Docker |
| **기타** | Chrome Extension, FFmpeg, Min-Cost Max-Flow |

---

## 개발 철학 (프로젝트를 통해 배운 것)

1. **문제에서 출발** — Med(동생 알레르기), Drafty(영어 이메일), AI SNS(콘텐츠 욕구)처럼 실제 불편함이 동기
2. **API는 초반에 검증** — Re:Cord에서 STT·DALL-E 제약을 뒤늦게 발견한 교훈
3. **대체 수단 준비** — 외부 API 정책 변경·장애에 대비한 폴백 설계
4. **비용·운영 고려** — Drafty API 비용, StocKKnock 캐싱·스케줄링으로 기능만큼 운영도 중요
