# PathFindManager

## 📌 목차
- [개요](#개요)
- [프로젝트 설명](#프로젝트-설명)
- [주요 기능 설명](#주요기능_설명)
- [테스트](#테스트)
- [폴더 구조](#폴더-구조)

---

## 개요

- **프로젝트 이름**: PathFindManager
- **개발 기간**: 2024.10 ~ 2024.11
- **개발 언어**: C++ , GDI
- **개발 인원**: 1명

---

## 프로젝트 설명

이 프로젝트는 **A*** 및 **Jump Point Search (JPS)** 알고리즘을 기반으로 한 경로 탐색 시각화 도구입니다.

윈도우즈 환경에서 C++와 Win32 API, GDI를 활용해 구현하였으며, 다양한 장애물 및 시작/목적지 설정 기능을 통해 실제 경로 탐색 과정을 **실시간으로 시각화**합니다.

사용자가 직접 장애물을 추가/삭제하고, 시작점 및 도착점을 지정하여 다양한 시나리오를 테스트할 수 있도록 합니다

---

## 주요 기능 설명

- 자동 길찾기

![Image](https://github.com/user-attachments/assets/8a124065-69f0-4c32-b0b2-79226fc78006)

- 한 단계씩 길찾기

()

| 입력 (Key/Mouse) | 동작 | 관련 메서드/설명 |
| --- | --- | --- |
| ↑, ↓, ←, → | 뷰 이동 | `MapTool::MoveUp/MoveDown/MoveLeft/MoveRight` MapManager |
| 마우스 휠 | 그리드 크기(배율) 조절 | `MapTool::SetScale` PathFindManager |
| 3 + 좌클릭 | 출발지 지정 | `MapTool::SetMap` (START) MapManager |
| 4 + 좌클릭 | 목적지 지정 | `MapTool::SetMap` (DEST) MapManager |
| 좌드래그 | 장애물 그리기 | `MapTool::SetMap` (OBSTACLE) MapManager |
| 우드래그 | 장애물 제거 | `MapTool::SetMap` (Erase) MapManager |
| 5 | 랜덤 장애물 배치 | `MapTool::SetRandomObstacles` MapManager |
| 6 | 모든 장애물 제거 | `MapTool::ClearObstacles` MapManager |
| 7 | 맵 전체를 장애물로 채움 | `MapTool::FillObstacles` MapManager |
| 1 | A* 알고리즘 선택 | `delete g_pPathFindManager; g_pPathFindManager = new AStar;` PathFindManager |
| 2 | JPS 알고리즘 선택 | `delete g_pPathFindManager; g_pPathFindManager = new JumpPointSearch;` PathFindManager |
| Enter | 전체 경로 탐색 | `PathFindAlgorithm::StartFindPath()` |
| Space | 단계별 경로 탐색 | `PathFindAlgorithm::FindPathStepInto()` |
| Q / W | 노드 생성 로그 ON/OFF | `PathFindAlgorithm::SetDebugCreateNode(true/false)` PathFindAlgorithm |
| A / S | 코너 탐지 로그 ON/OFF | `PathFindAlgorithm::SetDebugFindCorner(true/false)` PathFindAlgorithm |
| Z / X | OpenList 로그 ON/OFF | `PathFindAlgorithm::SetDebugOpenList(true/false)` PathFindAlgorithm |
| C / V | 경로 보정(코렉트) ON/OFF | `PathFindAlgorithm::SetCorrectPath(true/false)` PathFindAlgorithm |
| Backspace | 콘솔창 초기화 | `system("cls")` PathFindManager |

---

## 테스트

- **기능 테스트**
    - 수동 입력: 연속 범위(예: 1~N) 또는 랜덤 값 삽입/삭제 후 `PrintNodeData`, `PrintPathData`로 내부 상태 확인
    - 비교 모드 ON/OFF 전환 후 동일 입력 수행 → 삽입·삭제 성능 차이를 콘솔 로그로 비교
- **자동 테스트** (`TestTree` 기능)
    - `rand()`로 생성된 32비트 난수 삽입·삭제를 CHECKPOINT(5,000,000) 단위로 루프 반복
    - `TEST_RETURN::DOUBLE_RED`, `UNBALANCD` 오류 발생 시 즉시 중단 → 균형 검증
    - insert/delete 누적 성공 횟수 및 루프 카운트 결과 출력
---

## 폴더 구조

<pre> 
  📦 PathFindManager 
  ┣ 📂Framework # WinMain & 메시지 루프 
  ┃ ┣ 📜 PathFindManager.h 
  ┃ ┗ 📜 PathFindManager.cpp 
  ┣ 📂Core # 자료구조 구현 
  ┃ ┣ 📜 Pos.h 
  ┃ ┣ 📜 Pos.cpp 
  ┃ ┣ 📜 Node.h 
  ┃ ┣ 📜 Node.cpp 
  ┃ ┣ 📜 NodeMgr.h 
  ┃ ┗ 📜 NodeMgr.cpp 
  ┣ 📂Algorithm # 경로 탐색 알고리즘 
  ┃ ┣ 📜 PathFindAlgorithm.h 
  ┃ ┣ 📜 PathFindAlgorithm.cpp 
  ┃ ┣ 📜 Astar.h 
  ┃ ┣ 📜 Astar.cpp 
  ┃ ┣ 📜 JumpPointSearch.h 
  ┃ ┗ 📜 JumpPointSearch.cpp 
  ┣ 📂Map # 맵 상태 관리 & 렌더링 툴 
  ┃ ┣ 📜 Map.h 
  ┃ ┣ 📜 Map.cpp 
  ┃ ┣ 📜 MapManager.h 
  ┃ ┗ 📜 MapManager.cpp 
</pre>
