# Mini NPU Simulator — Learning Log

> CODYSSEY Foundation Program에서 MAC 연산과 패턴 분류를 구현하며 정리한 학습·트러블슈팅 기록입니다.

## Learning Scope | 학습 범위

- MAC (Multiply-Accumulate) 연산
- 중첩 반복문과 `O(N²)` 시간복잡도
- 부동소수점 비교와 epsilon
- JSON 기반 테스트 데이터
- 입력 검증과 예외 처리
- 모듈 분리와 import 경로

## MAC Operation | MAC 연산

외부 수치 연산 라이브러리에 의존하지 않고 순수 Python 반복문으로 입력 행렬과 필터를 비교했습니다. `N × N` 행렬의 모든 원소를 방문하므로 계산량은 `O(N²)`입니다.

단순히 결과를 얻는 것보다 **곱셈과 누산이 어떤 순서로 진행되는지 코드 수준에서 확인하는 것**을 학습 목표로 삼았습니다.

## Numerical Reliability | 수치 안정성

부동소수점 값을 직접 `==`로 비교하면 미세한 표현 오차 때문에 의도하지 않은 판정이 발생할 수 있습니다. 이를 피하기 위해 `1e-9` epsilon 기준을 적용했습니다.

두 점수의 차이가 epsilon 범위 안에 있으면 임의로 한쪽을 선택하지 않고 `Unknown`으로 처리했습니다. 이를 통해 계산 결과뿐 아니라 **판정 정책 자체도 프로그램 설계의 일부**라는 점을 배웠습니다.

## Input Validation | 입력 검증

- 잘못 입력한 행만 다시 입력
- 파싱 오류·길이 오류·범위 오류 메시지 분리
- 입력값을 `0`, `1`로 제한
- `Ctrl+C` 종료 시 traceback 미노출

사용자 입력을 받는 프로그램에서는 정상 입력만 가정하지 않고 잘못된 상태에서 어떻게 복구할지까지 설계해야 한다는 점을 확인했습니다.

## Test Analysis | 테스트 분석

JSON 분석 모드의 10개 테스트 중 8개가 PASS했고 2개는 판정 정책에 따라 기대값과 달랐습니다.

실패 결과를 숨기기보다 실제 MAC 점수와 epsilon 정책을 확인해 **왜 결과가 달라졌는지 설명하는 방식**으로 분석했습니다.

## Troubleshooting Log | 문제 해결 기록

### Floating-point comparison

직접 비교 대신 epsilon 기반 판정 규칙을 적용했습니다.

### File / Import typo

`reporter.py` 파일명 및 import 경로의 오타를 확인하고 수정했습니다.

### Module resolution

실행 위치에 따라 모듈을 찾지 못하는 문제를 경험한 뒤 프로젝트 루트에서 실행하고 명시적인 package import를 사용하는 방식으로 정리했습니다.

## What I Learned | 배운 점

이 프로젝트를 통해 NPU라는 용어 자체보다 **연산을 작은 단계로 분해해 직접 구현하고 검증하는 방법**을 익혔습니다. 알고리즘 복잡도, 수치 정밀도, 모듈 구조, 입력 검증과 UX가 작은 프로그램 안에서도 서로 연결되어 있다는 점을 배웠습니다.
