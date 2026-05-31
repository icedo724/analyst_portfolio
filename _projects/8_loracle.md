---
layout: page
title: "Loracle - 리그오브레전드 패치 예측 모델"
description: "8패치 데이터로 분류·회귀 모델 v6 학습 완료 — 데이터 누적 시 패치 방향 예측 정확도 검증 예정"
img: assets/img/proj_loracle.png
importance: 8
category: 개인
tags: [Python, 머신러닝, Riot API]
wip: true
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/Loracle"
    icon: "fab fa-github"
  - text: 리포트
    url: "https://www.notion.so/miniminimin/Loracle-32afbcdaed28807faab9f5c891532ffd"
    icon: "fa-solid fa-file-lines"
---

> **진행 중 (약 33%)** — 현재 8패치분 수집 완료, 목표 24패치(1년치)

## 배경 및 문제 정의

리그오브레전드는 약 2주마다 챔피언 능력치를 패치한다. 공식 발표 전 통계 데이터(승률·픽률·밴률)로 **다음 패치 방향을 예측**할 수 있는지 검증하는 것이 목표다.

핵심 난제: 패치당 변경 챔피언 수가 5~30명에 불과해, 전체의 **5% 미만이 변경**되는 극단적 클래스 불균형이 발생한다.

## 분석 방법

### 독립변수 설계 → 역방향 제거

초기 24개 후보에서 교차검증 기반 역방향 제거로 **8개**로 압축(F1 손실 0.018 이내):
`win_rate`, `pick_rate`, `ban_rate`, `op_index`, `position_entropy`, `win_rate_middle`, `pick_rate_delta`, `primary_position_BOTTOM`

### 모형 비교 (LightGBM vs XGBoost vs RandomForest)

패치 단위 Leave-One-Patch-Out 교차검증:

| 패치 | F1 Macro | 최적 모형 |
|---|---|---|
| 평균 (8패치) | 0.410 | — |
| 실전 기준 (16.8→16.9) | 0.343 | XGBoost |

{% include figure.liquid loading="eager" path="assets/img/chart_loracle_fi.png" class="img-fluid rounded" caption="특성 중요도 Top 6 및 패치별 LOPO CV F1 비교" %}

### 향상도 (Lift)

| 클래스 | 정밀도 | 기저율 | 향상도 |
|---|---|---|---|
| 버프 | 0.0% | 2.4% | 0배 |
| 너프 | 8.3% | 1.2% | **6.9배** |

너프 예측은 무작위 대비 **6.9배** 정확한 정보를 제공한다. 버프는 표본 4개 전부 탐지 실패 — 소수 클래스 누적 필요.

## 핵심 결과

- `op_index`(+1.107)가 가장 강한 단일 너프 신호 — 단순 승률이 아닌 승률×픽률 복합 지표가 Riot의 패치 기준에 더 가깝다는 근거
- 데이터 누적(24패치 목표)으로 버프·너프 소수 클래스 탐지 안정화 기대

