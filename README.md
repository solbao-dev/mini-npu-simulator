# Mini NPU Simulator

> A lightweight NPU simulation project that implements MAC operations and pattern classification from scratch.

**CODYSSEY · Foundation Program**  
`Python` `Algorithms` `MAC Operations` `JSON` `Error Handling`

## Overview

This project simulates **MAC (Multiply-Accumulate)** operations, one of the core computational ideas behind NPUs, and compares input patterns against filters to classify their shapes. The implementation focuses on explicit computation, numerical reliability, modular structure, and user-friendly input validation.

Rather than relying on NumPy, the core MAC operation is implemented directly in Python so that the underlying computation can be understood and explained.

## Architecture

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

- `main.py` — entry point and interaction flow
- `core/npu_core.py` — MAC computation, epsilon policy, and label normalization
- `data/data.json` — filters and test patterns
- `utils/reporter.py` — test and performance reporting

## Key Implementation

### MAC operation

The MAC calculation is implemented with nested loops without external numerical libraries. For an `N × N` matrix, every element is visited once, resulting in **O(N²)** time complexity.

### Numerical reliability

Floating-point comparisons use an epsilon of `1e-9`. When two scores differ by less than the threshold, the result is classified as `Unknown` rather than forcing an unreliable decision.

### Label normalization

Inputs such as `+`, `cross`, and `x` are normalized into consistent labels before comparison.

### Input validation & UX

- Invalid rows can be re-entered without restarting the entire input process.
- Parsing, length, and range errors use separate messages.
- Input values are restricted to `0` and `1` before computation.
- `Ctrl+C` exits cleanly without exposing a traceback.

## Results

The JSON analysis mode contains 10 test cases:

- **8 PASS**
- **2 policy-driven FAIL cases**

The two non-matching cases were analyzed rather than hidden: one pattern scores more strongly against the Cross filter despite its label, while another falls inside the epsilon threshold and is intentionally classified as `Unknown`.

## Troubleshooting

**Floating-point comparison** — replaced direct score comparison with an epsilon-based decision rule.

**Import/file naming errors** — corrected a `reporter.py` filename typo and made package paths explicit.

**Module resolution** — standardized execution from the project root and used explicit package imports.

## Run

```bash
python main.py
```

Choose:

```text
1  Keyboard input
2  JSON analysis
```

Example 3×3 Cross input:

```text
0 1 0
1 1 1
0 1 0
```

Expected classification: `Cross`.

## What I Learned

This project was an early step in my software-development journey: moving from using software to reasoning about computation directly. It helped me connect nested-loop complexity, numerical precision, modular architecture, validation, and user experience in one small system.

---

Part of my **CODYSSEY Foundation Program** learning journey.