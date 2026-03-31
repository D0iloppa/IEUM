# 🔗 IEUM (이움)
### **Iterative Execution Unit Manager**

> **"마디를 이어 흐름을 만들고, 반복을 통해 완성을 이룹니다."**

**IEUM**은 단순한 소프트웨어 매크로를 넘어, 하드웨어 레벨의 제어와 지능형 이미지 인식을 결합한 **자동화 파이프라인 구축 엔진**입니다. 사용자는 직관적인 GUI를 통해 복잡한 실행 단위(Unit)를 설계하고, 이를 안정적인 워크플로우로 통합하여 관리할 수 있습니다.

---

## 1. 🎯 Project Philosophy
* **연결(Connection):** 독립된 태스크들을 하나의 유기적인 파이프라인으로 연결합니다.
* **반복(Iteration):** 실행 단위(Unit)와 액션(Action)의 재귀적 반복을 통해 복잡한 로직을 단순화합니다.
* **정밀(Precision):** 하드웨어 입력 및 이미지 인식을 통해 환경에 구애받지 않는 정확한 자동화를 구현합니다.

---

## 2. 🏗 System Architecture

### **2.1. Process Model**
* **Main Process (GUI):** `pywebview` 기반의 UI 렌더링 및 사용자 이벤트 처리.
* **Worker Process (Agent):** 실제 매크로 로직이 수행되는 독립 프로세스. 메인 스레드 점유를 방지하고 긴급 중단(Emergency Stop)을 보장합니다.
* **IPC (Inter-Process Communication):** 메인 프로세스와 워커 간의 상태 공유 및 명령 전달.

### **2.2. Tech Stack**
* **Language:** Python 3.10+
* **Frontend:** HTML5, CSS3, JavaScript (React or Vue.js 추천)
* **Bridge:** `pywebview` (Python-JS Bridge)
* **Database:** SQLite (Embedded) + TinyDB (Task JSON Storage)
* **Hardware Interface:** `ctypes` / `cffi` (External DLL Loading)
* **Computer Vision:** `OpenCV`, `PyAutoGUI` / `MSS` (High-speed Screen Capture)
* **Hooking:** `pynput` / `keyboard` (Global Hotkeys)

---

## 3. 📋 Functional Specifications

### **3.1. Pipeline Structure**
1. **Project:** 최상위 관리 단위. 단일 프로젝트는 **단 하나의 Unique Workflow**를 가짐.
2. **Workflow:** 태스크들의 흐름도. 분기(Condition)와 루프(Loop)를 포함한 파이프라인.
3. **Task:** 실행의 최소 논리 단위. 내부 스크립트 또는 빌트인 액션으로 구성.
4. **Action:** 실제 물리적 동작(클릭, 키 입력, 이미지 대기 등). **액션 자체도 반복 및 그룹화 가능.**

### **3.2. Hardware & Image Control**
* **DLL Integration:** 소프트웨어 신호가 아닌 커널/하드웨어 레벨 입력을 위해 외부 `.dll` 파일을 로드하여 신호를 송출합니다.
* **Image Recognition:** * 화면 내 특정 이미지 탐색 및 좌표 반환.
    * 픽셀 값 변화 감지 및 임계값 설정.
    * ROI(Region of Interest) 설정을 통한 탐색 범위 최적화.

### **3.3. Execution & Shortcuts**
* **Global Hotkeys:** 프로그램이 백그라운드에 있어도 작동하는 실행/중지/일시정지 단축키 커스텀 설정.
* **Playback:** 전체 워크플로우 재생 및 특정 태스크 개별 재생 지원.

---

## 4. 🗄 Data Model (Schema)

### **Project & Workflow**
| Field | Type | Description |
| :--- | :--- | :--- |
| `p_id` | UUID | 프로젝트 고유 식별자 |
| `name` | String | 프로젝트 이름 |
| `flow_data` | JSON | 워크플로우 노드 및 엣지 정보 |
| `hotkey` | String | 프로젝트 실행 단축키 |

### **Task & Action**
| Field | Type | Description |
| :--- | :--- | :--- |
| `t_id` | UUID | 태스크 고유 식별자 |
| `type` | Enum | SCRIPT / BUILT-IN / LOOP |
| `content` | Text | 자체 스크립트 또는 액션 시퀀스 JSON |

---

## 5. 🚀 Development Roadmap

### **Phase 1: Foundation (Core Engine)**
* [ ] `pywebview` 기반 기본 윈도우 및 브릿지 설정.
* [ ] SQLite 기반 프로젝트 관리 스키마 구축.
* [ ] DLL 로딩 및 기본 하드웨어 입력 테스트 (Python `ctypes`).

### **Phase 2: Execution Intelligence**
* [ ] OpenCV 연동 이미지 템플릿 매칭 모듈 개발.
* [ ] 멀티프로세스 기반 워커 에이전트 구현.
* [ ] 전역 단축키 매핑 및 이벤트 리스너 등록.

### **Phase 3: GUI & Pipeline Builder**
* [ ] 노드 기반 워크플로우 에디터 개발.
* [ ] 태스크별 상세 설정 및 스크립트 편집기 구현.
* [ ] 실시간 실행 상태 모니터링 UI.

### **Phase 4: Optimization & Deployment**
* [ ] 업데이트 매니저 구현 (Version Check & Download).
* [ ] 리소스 최적화 (Memory Leak 점검).
* [ ] PyInstaller/Nuitka를 이용한 실행 파일 패키징.

---

## 6. 🛠 How to Contribute
1. **Fork** the repository.
2. Create your **Feature Branch**.
3. **Commit** your changes.
4. Push to the Branch and **Open a Pull Request**.