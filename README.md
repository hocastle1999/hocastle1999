### 👋 Hello, I'm hocastle1999

백엔드 개발자를 목표로 꾸준히 학습하고 기록하는 공간입니다.

---

### 🚀 Projects

#### 🗓️ [Reservation API](https://github.com/hocastle1999/reservation-api)

회의실 같은 공용 자원의 예약을 관리하는 REST API입니다. 동시 요청에서도 예약이 겹치지 않게 하는 **동시성 제어**를 핵심 과제로 다뤘습니다.

* 중복 예약 방지를 두 방식(`SELECT ... FOR UPDATE` 비관적 락, 30분 시간 칸 + 기본키)으로 구현하고 같은 테스트로 검증
* 부하 측정(32스레드, 960건)으로 두 방식 비교: 같은 시간대로 요청이 몰리면 락 방식 460건/초, 겹치지 않는 요청은 시간 칸 방식 269건/초
* 락을 걸었는데도 중복 예약이 생기는 문제를 동시 요청 테스트로 발견, 원인(REPEATABLE READ 스냅샷)을 찾아 READ COMMITTED로 해결
* JWT 인증과 Argon2id 비밀번호 해시, Alembic 마이그레이션, Docker 이미지와 CI까지 배포 준비
* `Python` `FastAPI` `MySQL` `SQLAlchemy` `Alembic` `pytest` `Docker` `GitHub Actions`

#### 🛗 [Smart Elevator](https://github.com/hocastle1999/smart-elevator)

엘리베이터 배차 알고리즘 시뮬레이터와 운행 모니터링 백엔드입니다. 하드웨어 없이 서버 안에서 엘리베이터를 시뮬레이션합니다.

* 상태 머신과 LOOK 운행 방식으로 만든 결정적 시뮬레이션 엔진 (같은 시드면 항상 같은 결과)
* Strategy 패턴으로 배차 전략 3개(Nearest Car, ETA 비용, 목적층 예약)를 구현하고 출근·점심·퇴근 교통 패턴에서 비교 실험. 출근 혼잡에서 평균 대기 346초 → 41초
* asyncio 시뮬레이션 루프, REST 호출, WebSocket 상태 방송으로 실시간 서버 구성
* 운행 기록을 MySQL에 저장하고 윈도 함수(`ROW_NUMBER`, `LEAD`, `RANK`)로 p95 대기 시간 등 통계 API 제공
* 고장 주입과 이상 감지, 자동 격리: 3분 넘게 기다린 승객 111명 → 0명
* `Python` `FastAPI` `asyncio` `WebSocket` `MySQL` `SQLAlchemy` `Alembic`

#### 📺 [Manager Workspace (Schedule Server)](https://github.com/hocastle1999/lshooooo-schedule-server)

SOOP 방송 매니저들이 함께 쓰는 웹사이트입니다. 방송 일정·공지·메모를 한곳에서 관리하고, 서버가 방송 채팅을 직접 받아 방송 도구를 제공합니다. 실제로 운영 중인 서비스입니다.

* SOOP 채팅 서버에 직접 접속하는 WebSocket 클라이언트를 Node.js로 구현, 후원 룰렛 명단과 방송 참여 중 매니저 표시에 사용
* 약 5만 건의 제재 기록을 수집해 참여자 제재 이력, 날짜별 제재 내역, 제재 순위 제공
* 외부 API의 요청 제한(429)에 맞춰 모든 요청을 한 줄로 세워 1.1초 간격으로 보내고, 사용자가 기다리는 요청은 앞에 끼워 넣는 큐 구성
* 방송국 공지와 e스포츠 일정을 주기적으로 크롤링, Upstash Redis에 저장하고 Render에 배포
* `Node.js` `Express` `WebSocket` `Upstash Redis` `Playwright` `Render`

#### 💻 [Manager Management Web Service](https://github.com/hocastle1999/manager-web)

Flask, MySQL, Ngrok 등을 활용한 웹 기반 인터넷 방송 매니저 관리 사이트입니다.

* Playwright 크롤러로 제재 내역을 수집해 MySQL에 중복 없이 저장, APScheduler로 5분마다 자동 동기화
* 매니저별·유저별 필터와 제재 횟수 순위 통계를 보여 주는 관리자 대시보드
* `Python` `Flask` `MySQL` `Playwright` `APScheduler` `Ngrok`

#### ⚽ [Football Kick Posture Analysis](https://github.com/hocastle1999/football-kick-analysis)

포즈 모델 기반 좌표 추출을 활용한 축구 킥 자세 교정 및 분석 시스템입니다.

* 스마트폰 영상에서 신체 주요 관절과 공의 좌표를 추출하고, LSTM으로 임팩트 전후 무게중심과 디딤발 위치 분석
* 동적 양자화로 모델을 경량화해 CPU 환경에서 실시간 추론
* `Python` `PyTorch` `MediaPipe BlazePose` `YOLOv8n`

#### 📂 Others

* [Terminal Hacker Simulation](https://github.com/hocastle1999/Hacking-simulation-game): Linux 명령어와 Shell Script로 미션을 해결하는 해킹 시뮬레이션 (`C++` `Bash` `Rocky Linux`)
* [EV Charging Station Database](https://github.com/hocastle1999/-DATABASE): 전기차 충전소 운영, 예약, 충전 내역을 관리하는 관계형 데이터베이스 설계 (`SQL`)

---

### 📚 Tech Stack & Study
* **Language**: Python (`PCCP` 준비 중), JavaScript (Node.js), SQL
* **Backend**: FastAPI, Flask, Express, SQLAlchemy, Alembic, WebSocket
* **Database**: MySQL, Redis (Upstash)
* **Test & DevOps**: pytest, ruff, GitHub Actions, Docker, Render, Linux
* **AI**: PyTorch, MediaPipe, YOLO
