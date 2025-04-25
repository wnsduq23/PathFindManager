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
- **개발 기간**: 2024.11 ~ 2024.12
- **개발 언어**: C++ , GDI
- **개발 인원**: 1명

---

## 프로젝트 설명

이 프로젝트는 **A*** 및 **Jump Point Search (JPS)** 알고리즘을 기반으로 한 경로 탐색 시각화 도구입니다.

윈도우즈 환경에서 C++와 Win32 API, GDI를 활용해 구현하였으며, 다양한 장애물 및 시작/목적지 설정 기능을 통해 실제 경로 탐색 과정을 **실시간으로 시각화**합니다.

사용자가 직접 장애물을 추가/삭제하고, 시작점 및 도착점을 지정하여 다양한 시나리오를 테스트할 수 있도록 합니다

---

## 주요 기능 설명

| 그룹           | 단축키 | 기능                             | 설명                                          |
| -------------- | :----: | -------------------------------- | --------------------------------------------- |
| **기본 노드 조작** | 1      | Search Node                      | 특정 값 검색                                   |
|                | 2      | Insert Node                      | 연속 범위(시작→끝) 삽입                         |
|                | 5      | Delete Node                      | 연속 범위(시작→끝) 삭제                         |
| **랜덤 노드 조작** | 3      | Insert Random Node (≤9999)       | 0~9998 사이 난수 N개 삽입                      |
|                | 4      | Insert Random Node (≤INT_MAX)    | 31비트 난수 N개 삽입                           |
|                | 6      | Delete Random Node               | 트리에서 랜덤 N개 삭제                         |
| **출력·검사**     | 7      | Print Node Data                  | 중위 순회 결과 값 목록 출력                    |
|                | 8      | Print Path Data                  | 각 리프 경로별 black/red 카운트 출력             |
| **테스트·비교**   | 9      | Test Tree                        | 자동 삽입·삭제 무결성 테스트                    |
|                | 0      | Set Compare Mode                 | RB-Tree ↔ BST 동기화 모드 토글                 |
|                | Q      | Print Compare Result             | RB vs BST 성능 콘솔 출력 및 `output.txt` 저장 |
|                | W      | Shift Tree Drawing               | 화면 트리 드로잉(RB-Tree/BST) 전환             |

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
