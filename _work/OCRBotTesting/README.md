# OCRBotTesting

Mac App Store 숨은그림찾기 게임용 자동 클릭 봇입니다. 화면 하단의 한국어 단어를 OCR로 읽고, 미리 저장된 좌표로 자동 클릭합니다.

| 항목 | 내용 |
|------|------|
| **상태** | 개발 완료 |
| **유형** | 개인 프로젝트 (학습·테스트 목적) |
| **플랫폼** | macOS 전용 |

---

## 소개

EasyOCR로 게임 화면 하단의 한국어 단어를 인식하고, `coord_map.json`에 저장된 좌표로 자동 클릭하는 Python 봇입니다. OCR + 화면 캡처 + 마우스 제어를 결합한 자동화 실험 프로젝트입니다.

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| **좌표 매핑** | `map_coords.py`로 게임 아이템 35개의 화면 좌표 기록 |
| **한국어 OCR** | EasyOCR로 화면 하단 단어 바 인식 |
| **자동 클릭** | 인식된 단어와 좌표 매칭 후 pyautogui로 클릭 |
| **인간형 딜레이** | 클릭 간 0.3~0.8초 랜덤 딜레이 |

---

## 기술 스택

| 영역 | 기술 |
|------|------|
| **Language** | Python 3.10+ |
| **OCR** | EasyOCR (한국어) |
| **화면 캡처** | mss |
| **입력 제어** | pyautogui, pynput |
| **이미지** | Pillow, numpy |

---

## 프로젝트 구조

```
OCRBotTesting/
├── bot.py            # 메인 봇 스크립트
├── map_coords.py     # 좌표 매핑 도우미
├── coord_map.json    # 자동 생성되는 좌표 사전
├── requirements.txt  # 의존성
└── docs/             # 문서
```

---

## 시작하기

### 사전 요구사항

- Python 3.10+
- macOS
- **손쉬운 사용(Accessibility)** 권한 — Terminal 또는 IDE
- **화면 기록(Screen Recording)** 권한 — Terminal

> `시스템 설정 → 개인 정보 보호 및 보안 → 손쉬운 사용 / 화면 기록`에서 허용

### 1. 설치

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. 좌표 매핑 (처음 한 번)

1. `map_coords.py` 상단 `ITEM_NAMES`를 실제 게임 단어로 수정
2. 실행:

```bash
python3 map_coords.py
```

3. 3초 안에 게임 창으로 전환
4. 안내하는 단어의 아이템을 화면에서 클릭 (35개)
5. 완료 시 `coord_map.json` 자동 저장 (ESC로 중간 저장 가능)

### 3. 캡처 영역 조정

`bot.py`의 `CAPTURE_REGION`을 게임 창 하단 단어 바에 맞게 수정:

```python
CAPTURE_REGION = {
    "top": 1300,
    "left": 400,
    "width": 1200,
    "height": 120,
}
```

### 4. 봇 실행

```bash
python3 bot.py
```

3초 카운트다운 후 게임 창으로 전환하면 자동 클릭이 시작됩니다.

---

## 설정값 (`bot.py`)

| 변수 | 기본값 | 설명 |
|------|--------|------|
| `COORD_MAP_FILE` | `coord_map.json` | 좌표 파일 경로 |
| `CAPTURE_REGION` | 화면 하단 | OCR 캡처 영역 |
| `OCR_CONFIDENCE_THRESHOLD` | `0.4` | 이 값 미만 OCR 결과 무시 |
| `CLICK_DELAY_MIN/MAX` | `0.3` / `0.8` s | 클릭 간 랜덤 딜레이 |
| `CLICKS_PER_ROUND` | `26` | 한 라운드 클릭 횟수 |
| `STARTUP_DELAY` | `3` s | 시작 전 대기 |

---

## 문제 해결

| 증상 | 해결책 |
|------|--------|
| `PermissionError` / 클릭 안 됨 | 손쉬운 사용 권한 확인 |
| 화면 캡처 실패 | 화면 기록 권한 확인 |
| OCR 정확도 낮음 | `CAPTURE_REGION` 재조정, 게임 창 최대화 |
| 단어는 읽히나 클릭 안 됨 | `coord_map.json` 단어 철자 일치 확인 |
| EasyOCR 첫 실행 느림 | 모델 다운로드 중 (정상, 1회) |

---

## 참고

- 개인 학습 및 테스트 목적으로 제작되었습니다.
- 게임 서비스 약관을 확인하고 사용하세요.
