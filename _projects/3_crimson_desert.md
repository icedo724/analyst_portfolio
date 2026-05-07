---
layout: page
title: 시계열 회귀 기반 신규 출시 서비스 만족도 분석 (붉은사막)
description: 출시 후 6주 만족도 추세를 AAA 출시작 2종과 정량 비교 — NLP 감성 분류 + 시계열 회귀로 패치 효과 입증
img: assets/img/proj_crimson.png
importance: 2
category: 개인
tags: [Python, NLP, 시계열, 회귀 분석]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/crimson_desert_review"
    icon: "fab fa-github"
  - text: 리포트
    url: "https://www.notion.so/miniminimin/358fbcdaed28804e92f6c73ecc6fa899"
    icon: "fa-solid fa-file-lines"
---

출시 후 6주간 Steam 리뷰 **71,000건(본 IP) + 376,000건(벤치마크)** 전수 분석.

## 배경 및 문제 정의

신규 IP의 런치 이후 만족도 추세를 어떻게 객관적으로 추적할 것인가?
단순 별점 비율이 아닌 **패치별·속성별·플레이타임별** 분해 지표로 퀄리티 저하를 조기 탐지하는 프레임워크를 설계했다.

## 데이터

| 게임 | 리뷰 수 | 기간 |
|---|---|---|
| 붉은사막 | 한국어 10,792 / 영어 60,206 | 출시 후 42일 |
| Elden Ring (벤치) | 220,000 | 출시 후 42일 |
| Cyberpunk 2077 (벤치) | 155,000 | 출시 후 42일 |

## 분석 방법

### 1단계 — 패치별 긍정률 시계열

Steam appreviews API로 전수 수집 후 패치 윈도우별로 집계, 95% 신뢰구간 산출.

{% include figure.liquid loading="eager" path="assets/img/chart_crimson_sentiment.png" class="img-fluid rounded" caption="패치 윈도우별 긍정률 추이 (KR/EN, 95% CI)" %}

| 패치 | KR 긍정률 | EN 긍정률 |
|---|---|---|
| 출시 (1.00.00) | 63.9% | 80.2% |
| 핫픽스 (1.00.03) | 89.7% | 90.3% |
| 1.01.00 | 90.2% | 90.2% |
| 1.04.00 | 88.3% | 84.6% ⚠️ |

### 2단계 — 핫픽스 시점 효과 (시계열 회귀)

1.00.03 핫픽스 시점을 개입점으로 설정한 단절적 시계열 회귀. R² = 0.91(KR) / 0.83(EN).

핵심 발견: 핫픽스 즉각 점프는 유의하지 않았고, **회복 추세가 안정 구간에 진입하는 시점**이 출시 후 4~5일임을 통계적으로 입증.

### 3단계 — 속성별 분해

{% include figure.liquid loading="eager" path="assets/img/chart_crimson_aspect.png" class="img-fluid rounded" caption="속성별 긍정률 히트맵 (패치 × 속성)" %}

키워드 매칭으로 5개 속성(조작/전투, 스토리/세계관, 그래픽, 성능/최적화, 가격/가성비)의 긍정률을 산출.

**글로벌 Alert**: 성능/최적화 EN 긍정률 76% → 57% (-17.4%p), 1.04.00 패치 후 linux/broke 키워드 급부상 → 패치 회귀 의심.

### 4단계 — 벤치마크 비교

| 지표 | 붉은사막 | Elden Ring | Cyberpunk |
|---|---|---|---|
| 6주 누적 긍정률 (EN) | 86% | 92% | 83% |
| 회복 속도 (KR, %p/일) | +1.43 | +0.90 | -0.30 |

## 핵심 결과

- 회복 속도는 Elden Ring의 **1.6배** — 핫픽스 대응 효과 정량 입증
- 리뷰 좋아요 가중 시 EN 만족도 추가 -4.7%p → 잠재 구매자 노출 인상에 직접 위협
- 0~5h 단기 체험 긍정률 49.6% vs 20~50h 91.5% — 초반 진입 경험 개선 필요

## 회고

대규모 텍스트 데이터를 직접 수집·전처리하고 단일 지표(만족도)를 다층으로 분해한 경험. 속성 분류 정확도(커버리지 64.4%)와 다중 검정 보정 미적용이 남은 한계다.

