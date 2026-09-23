# Mini NPU Simulator

> **A lightweight NPU simulation project implementing MAC operations and pattern classification from scratch.**  
> MAC 연산과 패턴 분류 과정을 직접 구현하며 NPU의 기초 연산 원리를 학습한 시뮬레이션 프로젝트

**CODYSSEY · Foundation Program | 입학연수 과정**  
`Python` `Algorithms` `MAC Operations` `JSON` `Error Handling`

---

## Overview | 프로젝트 소개

This project simulates **MAC (Multiply-Accumulate)** operations, one of the core computational ideas behind NPUs, and compares input patterns against filters to classify their shapes.

NPU의 핵심 연산 개념 중 하나인 **MAC(Multiply-Accumulate)**을 직접 구현하고 입력 패턴과 필터의 점수를 비교하여 형태를 판정합니다. NumPy에 의존하지 않고 순수 Python 반복문으로 계산 과정을 구현하여 내부 연산을 이해하고 설명하는 데 초점을 맞췄습니다.

## Key Implementation | 핵심 구현

- MAC computation with nested loops | 2중 반복문 기반 MAC 연산
- `O(N²)` matrix traversal | 행렬 연산의 시간복잡도 확인
- `1e-9` epsilon policy | 부동소수점 오차를 고려한 판정
- JSON-based test analysis | JSON 테스트 데이터 분석
- Input validation and recovery | 입력 오류 검증과 재입력 흐름
- Modular project structure | 연산·데이터·리포팅 역할 분리

## Project Structure | 프로젝트 구조

```text
mini-npu-simulator/
├── main.py
├── core/
│   └── npu_core.py
├── data/
│   └── data.json
├── utils/
│   └── reporter.py
├── docs/
│   └── LEARNING_LOG.md
└── README.md
```

## Run | 실행 방법

```bash
python main.py
```

```text
1  Keyboard input
2  JSON analysis
```

Example 3×3 Cross input | 3×3 Cross 입력 예시:

```text
0 1 0
1 1 1
0 1 0
```

Expected classification | 예상 결과: `Cross`

## Learning Focus | 학습 포인트

This project was an early step from using software to reasoning about computation directly.

개발 초기 단계에서 단순히 프로그램을 사용하는 것을 넘어 **연산이 내부에서 어떻게 이루어지는지 직접 구현하고 설명하는 경험**을 했습니다. 특히 알고리즘 복잡도와 수치 정밀도, 입력 검증이 실제 프로그램의 결과에 어떤 영향을 주는지 확인했습니다.

## Learning Log | 상세 학습 기록

MAC 연산, epsilon 판정 정책, 테스트 분석과 import/모듈 문제 해결 과정은 별도의 Learning Log에 보존했습니다.

➡️ **[View Detailed Learning Log](./docs/LEARNING_LOG.md)**

---

**CODYSSEY AI All-in-One · Foundation Program**