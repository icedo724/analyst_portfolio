---
layout: page
title: 게임 패치 방향 예측 ML 모델 — Loracle (진행 중)
description: API 수집 데이터로 분류·회귀 모델 v5 학습 — 패치 대상 분류 + 스탯 변화폭 회귀 파이프라인
img: assets/img/proj_loracle.png
importance: 8
category: 개인
tags: [Python, 머신러닝, Riot API]
related_publications: false
---

> **진행 중 (약 29%)** — 현재 7패치분 수집 완료, 목표 24패치(1년치)

## 배경 및 문제 정의

리그오브레전드는 약 2주마다 챔피언 능력치를 패치한다. 공식 발표 전 통계 데이터(승률·픽률·밴률)로 **다음 패치 방향을 예측**할 수 있는지 검증하는 것이 목표다.

핵심 난제: 패치당 변경 챔피언 수가 5~30명에 불과해, 전체의 **5% 미만이 변경**되는 극단적 클래스 불균형이 발생한다.

## 분석 방법

### 독립변수 설계 → 역방향 제거

초기 24개 후보에서 교차검증 기반 역방향 제거로 **6개**로 압축(F1 손실 0.016 이내):
`win_rate`, `op_index`, `ban_delta`, `win_rate_middle`, `last_label`, `patch_num`

### 모형 비교 (LightGBM vs XGBoost vs RandomForest)

패치 단위 Leave-One-Patch-Out 교차검증:

| 패치 | F1 Macro | 최적 모형 |
|---|---|---|
| 평균 (7패치) | 0.409 | — |
| 실전 기준 (16.7→16.8) | 0.356 | LightGBM |

{% include figure.liquid loading="eager" path="assets/img/chart_loracle_fi.png" class="img-fluid rounded" caption="특성 중요도 Top 6 및 패치별 LOPO CV F1 비교" %}

### 향상도 (Lift)

| 클래스 | 정밀도 | 기저율 | 향상도 |
|---|---|---|---|
| 버프 | 7.1% | 1.8% | **3.9배** |
| 너프 | 4.2% | 1.6% | **2.7배** |

F1이 낮아 보이지만, 무작위 추정 대비 3~4배 정확한 정보를 제공한다.

## 핵심 결과

- `win_rate`(+0.633)·`op_index`(+0.603)이 너프 예측의 핵심 변수 — "강하면 너프"라는 직관과 일치
- 데이터 누적(24패치 목표)으로 버프·너프 소수 클래스 탐지 안정화 기대

**결과물**: [GitHub](https://github.com/icedo724/Loracle) · [리포트](https://www.notion.so/miniminimin/Loracle-32afbcdaed28807faab9f5c891532ffd)
