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

![Image](https://github.com/user-attachments/assets/ee911288-d9a7-4746-8361-0366bbf32a59)

| 입력 (Key/Mouse) | 동작 | 관련 메서드/설명 |
| --- | --- | --- |
| ↑, ↓, ←, → | 뷰 이동 | `MapTool::MoveUp/MoveDown/MoveLeft/MoveRight`  |
| 마우스 휠 | 그리드 크기(배율) 조절 | `MapTool::SetScale` |
| 3 + 좌클릭 | 출발지 지정 | `MapTool::SetMap` (START)  |
| 4 + 좌클릭 | 목적지 지정 | `MapTool::SetMap` (DEST)  |
| 좌드래그 | 장애물 그리기 | `MapTool::SetMap` (OBSTACLE)  |
| 우드래그 | 장애물 제거 | `MapTool::SetMap` (Erase)  |
| 5 | 랜덤 장애물 배치 | `MapTool::SetRandomObstacles` r |
| 6 | 모든 장애물 제거 | `MapTool::ClearObstacles`  |
| 7 | 맵 전체를 장애물로 채움 | `MapTool::FillObstacles`  |
| 1 | A* 알고리즘 선택 | `delete g_pPathFindManager; g_pPathFindManager = new AStar;`  |
| 2 | JPS 알고리즘 선택 | `delete g_pPathFindManager; g_pPathFindManager = new JumpPointSearch;`  |
| Enter | 전체 경로 탐색 | `PathFindAlgorithm::StartFindPath()` |
| Space | 단계별 경로 탐색 | `PathFindAlgorithm::FindPathStepInto()` |
| Q / W | 노드 생성 로그 ON/OFF | `PathFindAlgorithm::SetDebugCreateNode(true/false)`  |
| A / S | 코너 탐지 로그 ON/OFF | `PathFindAlgorithm::SetDebugFindCorner(true/false)`  |
| Z / X | OpenList 로그 ON/OFF | `PathFindAlgorithm::SetDebugOpenList(true/false)`  |
| C / V | 경로 보정(코렉트) ON/OFF | `PathFindAlgorithm::SetCorrectPath(true/false)`  |
| Backspace | 콘솔창 초기화 | `system("cls")`  |

---

## 테스트

1. **기본 동작 테스트**
    - 빈 맵, 장애물 맵, 대각선 장애물 등 다양한 맵에서 A*와 JPS 모두 정상적으로 경로를 찾아내는지 확인했습니다.
2. **극한 케이스**
    - 출발지와 목적지가 같을 때 즉시 종료 메시지를 출력하는지 확인했습니다.
    - 완전 장애물 맵에서 “Can't Find Path!” 메시지가 표시되는지 확인했습니다.
3. **성능 측정**
    - 100×100, 200×200 그리드에서 각각 전체 탐색 시간을 측정했습니다.
    - JPS가 A*보다 평균 30% 이상 빠르게 동작함을 확인했습니다.
4. **메모리/안정성**
    - SetData() 호출 전후로 메모리 누수를 검사했습니다.
    - NodeMgr 내 리스트 초기화가 정상적으로 동작함을 확인했습니다.
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
