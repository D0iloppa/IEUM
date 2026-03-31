# 🔗 IEUM (이움)
### **Iterative Execution Unit Manager**

> **"마디를 이어 흐름을 만들고, 반복을 통해 완성을 이룹니다."**

**IEUM**은 단순한 소프트웨어 매크로를 넘어, 하드웨어 레벨의 제어와 지능형 이미지 인식을 결합한 **자동화 파이프라인 구축 엔진**입니다. 사용자는 직관적인 GUI를 통해 복잡한 실행 단위(Unit)를 설계하고, 이를 안정적인 워크플로우로 통합하여 관리할 수 있습니다.

---

## 1. 🎯 Project Philosophy
* **연결(Connection):** 독립된 태스크들을 하나의 유기적인 파이프라인으로 연결합니다.
* **반복(Iteration):** 실행 단위(Unit)와 액션(Action)의 재귀적 반복을 통해 복잡한 로직을 단순화합니다.
* **정밀(Precision):** 하드웨어 레벨(DLL) 입력 및 OpenCV 이미지 인식을 통해 환경에 구애받지 않는 정확한 자동화를 구현합니다.

---

## 2. 🏗 System Architecture

### **2.1. Process Model**
* **Main Process (GUI):** `pywebview` 기반의 UI 렌더링 및 사용자 이벤트 처리.
* **Worker Process (Agent):** 실제 매크로 로직이 수행되는 독립 프로세스. 메인 스레드 점유를 방지하고 긴급 중단(Emergency Stop)을 보장합니다.
* **IPC (Inter-Process Communication):** 메인 프로세스와 워커 간의 상태 공유 및 명령 전달.

### **2.2. Tech Stack**
* **Language:** Python 3.10+
* **Frontend:** React + Vite (Node.js는 빌드 시에만 활용)
* **Bridge:** `pywebview` (Python-JS Bridge)
* **Database:** SQLite (Embedded) + TinyDB (Task JSON Storage)
* **Hardware Interface:** `ctypes` (External DLL Loading)
* **Computer Vision:** `OpenCV`, `PyAutoGUI` / `MSS`
* **Hooking:** `pynput` (Global Hotkeys)

---

## 📂 3. Directory Structure

```text
IEUM/
├── assets/                # 아이콘 및 이미지 인식용 템플릿
├── bin/                   # 하드웨어 제어용 외부 DLL (.dll)
│   └── x64/               # 64비트용 바이너리 (Git 추적 대상)
├── docs/                  # 설계 문서 및 매뉴얼
│   └── ai/                # AI 협업 로그 (Git Ignore 대상)
├── src/                   # Python 백엔드 소스
│   ├── main.py            # 진입점
│   ├── bridge/            # Python-JS 통신 레이어
│   ├── core/              # 실행 엔진 및 워커 로직
│   ├── driver/            # DLL 로더 및 비전 모듈
│   └── database/          # SQLite 관리 모듈
├── gui/                   # React 프론트엔드 (Vite 환경)
│   ├── src/               # React 컴포넌트 및 로직
│   ├── dist/              # 빌드 결과물 (Python 로드 대상)
│   └── node_modules/      # 개발용 패키지
├── tests/                 # 단위 테스트
├── venv/                  # 파이썬 가상환경
├── .gitignore             # Git 제외 목록 (.dll 포함 설정)
├── venv_activate.sh       # 가상환경 활성화 단축 스크립트
└── README.md              # 프로젝트 명세서
```

---

## 🛠 4. Getting Started

### **4.1. Python 가상환경 설정**
본 프로젝트는 독립된 환경을 위해 `venv`를 사용합니다. 루트 디렉토리에 생성된 `venv_activate.sh`를 통해 간편하게 활성화할 수 있습니다.

```bash
# 가상환경 활성화 (Git Bash 기준)
source venv_activate.sh

# 필수 패키지 설치
pip install -r requirements.txt
```

### **4.2. Frontend 개발 환경 (Vite)**
UI 수정이 필요한 경우 `gui` 폴더 내에서 작업을 수행합니다.

```bash
cd gui
npm install
npm run dev   # Vite 개발 서버 실행
npm run build # 최종 결과물 생성 (Python에서 호출되는 static 파일)
```

---

## 📋 5. Functional Specifications

### **5.1. Pipeline Structure**
1. **Project:** 최상위 관리 단위. 단일 프로젝트는 **단 하나의 Unique Workflow**를 가짐.
2. **Workflow:** 태스크들의 흐름도. 분기와 루프를 포함한 파이프라인.
3. **Task:** 실행의 최소 논리 단위. 내부 스크립트 또는 빌트인 액션으로 구성.
4. **Action:** 실제 물리적 동작(클릭, 키 입력 등). **액션 자체도 반복 및 그룹화 가능.**

### **5.2. Hardware & Image Control**
* **DLL Integration:** 커널 레벨 입력을 위해 `bin/x64/`에 위치한 외부 `.dll`을 로드하여 정밀한 신호 송출.
* **Image Recognition:** OpenCV 기반 템플릿 매칭 및 픽셀 감지 지원. ROI 설정을 통한 성능 최적화.

### **5.3. Hotkeys & Playback**
* **Global Hotkeys:** 백그라운드 상태에서도 작동하는 전역 단축키(실행/중지/일시정지).
* **Playback:** 전체 워크플로우 재생 및 특정 태스크/액션 단위의 개별 테스트 재생 지원.

---

## 🚀 6. Development Roadmap

* **Phase 1:** `pywebview` 기초 설정 및 `ctypes` 기반 DLL 로딩/입력 기능 검증.
* **Phase 2:** OpenCV 이미지 인식 모듈화 및 멀티프로세스 워커 에이전트 연동.
* **Phase 3:** React 기반 노드 에디터 UI 개발 및 Python-JS 통신 브릿지 고도화.
* **Phase 4:** 자동 업데이트 시스템 구축 및 PyInstaller를 이용한 `.exe` 패키징.

---

## 📄 7. License
This project is licensed under the MIT License.