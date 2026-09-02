# HotelBooker

복잡한 DB 설계·관리 연습을 목적으로 만든 호텔 객실 예약 시스템입니다. 사용자 예약부터 관리자 대시보드, 결제, 리뷰까지 호텔 운영에 필요한 기능을 포함합니다.

| 항목 | 내용 |
|------|------|
| **상태** | 개발 완료 |
| **유형** | 개인 프로젝트 (1인 풀스택) |
| **목적** | 예약·결제·리뷰·관리자 권한이 얽힌 DB 스키마 설계 연습 |

---

## 소개

HotelBooker는 JWT 기반 인증, 객실 예약·결제, 리뷰, 관리자 대시보드를 갖춘 풀스택 호텔 예약 웹 서비스입니다. 사용자/관리자 역할 분리와 복잡한 엔티티 관계를 직접 설계·구현하는 데 초점을 맞췄습니다.

---

## 주요 기능

| 구분 | 기능 |
|------|------|
| **사용자** | 회원가입·로그인 (JWT), 아이디/비밀번호 찾기 (이메일 인증) |
| | 객실 조회 (목록, 상세, 이미지), 예약·조회·취소 |
| | 결제 (카드, 계좌이체, 현금), 리뷰·평점 작성 |
| | 마이페이지 (예약 내역, 리뷰 관리), 공지사항 |
| **관리자** | 대시보드 (예약·체크인·체크아웃, 객실 상태, 월별 매출) |
| | 객실 CRUD, 예약 상태 변경, 리뷰 공개/비공개·관리자 답변 |
| | 공지사항 관리, 기간별 통계·매출 분석 |

---

## 기술 스택

| 영역 | 기술 |
|------|------|
| **Backend** (`bookBE`) | Spring Boot 3.3.4, Java 17, Spring Data JPA, Spring Security + JWT |
| **Frontend** (`bookFE`) | React 19, Vite 7, Tailwind CSS, React Router, Axios |
| **Database** | PostgreSQL |
| **API 문서** | SpringDoc OpenAPI (Swagger) |
| **이메일** | Spring Mail (Gmail SMTP) |

---

## 시스템 구조

```
React (bookFE)          Spring Boot (bookBE)       PostgreSQL
localhost:5173  ──REST──▶  localhost:8080    ──▶  hoteldb
```

---

## 프로젝트 구조

```
HotelBooker/
├── bookBE/                 # 백엔드 (Spring Boot)
│   └── src/main/java/com/hotel/booking/
│       ├── auth/           # 인증, 회원가입, 계정 복구
│       ├── booking/        # 예약 관리
│       ├── payment/        # 결제
│       ├── review/         # 리뷰
│       ├── room/           # 객실
│       ├── admin/          # 관리자 기능
│       └── notice/         # 공지사항
├── bookFE/                 # 프론트엔드 (React)
│   └── src/pages/          # Home, Login, Rooms, Booking, AdminDashboard 등
└── HOTEL_BOOKING_SYSTEM_DOCUMENTATION.md  # 상세 기술 문서
```

---

## 시작하기

### 사전 요구사항

- Java 17+
- Node.js 18+
- PostgreSQL 12+

### 1. 데이터베이스

```sql
CREATE DATABASE hoteldb;
```

### 2. 백엔드

```bash
cd bookBE
# application.properties 또는 application.yml에서 DB 연결 정보 수정
./gradlew bootRun
```

- 서버: `http://localhost:8080`
- Swagger: `http://localhost:8080/swagger-ui.html`

### 3. 프론트엔드

```bash
cd bookFE
npm install
npm run dev
```

- 앱: `http://localhost:5173`

### 환경 설정 (bookBE)

| 항목 | 설명 |
|------|------|
| `spring.datasource.url` | `jdbc:postgresql://localhost:5432/hoteldb` |
| `spring.datasource.username` | DB 사용자명 |
| `spring.datasource.password` | DB 비밀번호 |
| JWT 설정 | `application.yml`에서 관리 |
| Mail 설정 | Gmail SMTP (`application.yml`) |

> 상세: `HOTEL_BOOKING_SYSTEM_DOCUMENTATION.md` 참고

---

## API 문서

Swagger UI에서 전체 API를 확인할 수 있습니다.

`http://localhost:8080/swagger-ui.html`

---

## 참고

- 예약·결제·리뷰·관리자 권한이 얽힌 **복잡한 DB 스키마** 설계 경험
- Swagger로 API 문서화하여 프론트·백엔드 연동 효율화
