# Mini NPU Simulator

> A lightweight NPU simulation project that implements MAC operations and pattern classification from scratch.  
> MAC 연산과 패턴 분류 과정을 직접 구현하며 NPU의 기초 연산 원리를 학습한 시뮬레이션 프로젝트입니다.

**CODYSSEY · Foundation Program | 입학연수 과정**  
`Python` `Algorithms` `MAC Operations` `JSON` `Error Handling`

## Overview | 프로젝트 소개

This project simulates **MAC (Multiply-Accumulate)** operations, one of the core computational ideas behind NPUs, and compares input patterns against filters to classify their shapes.

NPU의 핵심 연산 개념 중 하나인 **MAC(Multiply-Accumulate)**을 직접 구현하고 입력 패턴과 필터의 점수를 비교하여 형태를 판정합니다. NumPy에 의존하지 않고 순수 Python 반복문으로 계산 과정을 구현하여 내부 연산을 이해하고 설명할 수 있도록 하는 데 초점을 맞췄습니다.

## Architecture | 구조

```text
mini-npu-simulator/
├── main.py
├── core/
│   └── npu_core.py
├── data/
│   └── data.json
└── utils/
    └── reporter.py
```

- `main.py` — entry point and interaction flow | 실행 진입점과 사용자 흐름
- `core/npu_core.py` — MAC computation, epsilon policy, label normalization | 핵심 연산과 판정 정책
- `data/data.json` — filters and test patterns | 필터와 테스트 패턴
- `utils/reporter.py` — test and performance reporting | 테스트·성능 결과 출력

## Key Implementation | 핵심 구현

### MAC Operation | MAC 연산

The MAC calculation uses nested loops without external numerical libraries. For an `N × N` matrix, the time complexity is **O(N²)**.

외부 수치 연산 라이브러리 없이 2중 반복문으로 직접 계산했습니다. `N × N` 행렬의 모든 원소를 방문하므로 시간 복잡도는 **O(N²)**입니다.

### Numerical Reliability | 수치 안정성

Floating-point comparisons use an epsilon of `1e-9`. Scores inside the threshold are classified as `Unknown` instead of forcing an unreliable result.

부동소수점 오차를 고려해 `1e-9`의 epsilon 기준을 적용했습니다. 두 점수의 차이가 기준보다 작으면 억지로 결과를 결정하지 않고 `Unknown`으로 처리합니다.

### Input Validation & UX | 입력 검증과 UX

- Invalid rows can be re-entered without restarting. | 잘못 입력한 행만 다시 입력 가능
- Parsing, length, and range errors use separate messages. | 파싱·길이·범위 오류 메시지 분리
- Input values are restricted to `0` and `1`. | 입력값을 `0`, `1`로 제한
- `Ctrl+C` exits without exposing a traceback. | 강제 종료 시 traceback 없이 종료

## Results | 결과

The JSON analysis mode contains 10 test cases: **8 PASS** and **2 policy-driven FAIL cases**.

JSON 분석 모드의 10개 테스트 중 **8개가 PASS**했고, 2개는 단순 오류로 숨기지 않고 판정 정책에 따라 왜 결과가 달라졌는지 분석했습니다. 하나는 실제 MAC 점수가 Cross 필터에 더 높았고, 다른 하나는 epsilon 범위 안에 들어 `Unknown`으로 판정된 경우입니다.

## Troubleshooting | 트러블슈팅

- **Floating-point comparison | 부동소수점 비교** — direct comparison → epsilon-based decision rule
- **File/import typo | 파일명·Import 오류** — `reporter.py` 오타 수정 및 경로 명시
- **Module resolution | 모듈 인식** — 프로젝트 루트 실행과 명시적 package import로 표준화

## Run | 실행

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

## What I Learned | 배운 점

This project was an early step from using software to reasoning about computation directly. It connected algorithmic complexity, numerical precision, modular architecture, validation, and user experience in one small system.

개발을 시작한 초기 단계에서 단순히 프로그램을 사용하는 것을 넘어 **연산이 내부에서 어떻게 이루어지는지 직접 구현하고 설명하는 경험**을 했습니다. 알고리즘 복잡도, 수치 정밀도, 모듈 구조, 예외 처리와 사용자 입력 경험이 하나의 프로그램 안에서 어떻게 연결되는지 배웠습니다.

---

Part of my **CODYSSEY Foundation Program | 코디세이 입학연수 과정**.