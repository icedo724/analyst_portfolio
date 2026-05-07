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

게임 패치 방향성을 예측하는 머신러닝 모델 (진행 중).

**접근**
- Riot API로 챔피언별 통계 데이터 수집 (현재 7패치분 누적)
- 분류 모델 (패치 대상 / 비대상)
- 회귀 모델 (스탯 변화 폭 예측)
- 모델 v5 학습 완료, 24패치(1년치) 수집 후 예측 정확도 검증 예정

**도구**: Python · Riot API · 분류 모델 · 회귀 모델

**결과물**
- [GitHub](https://github.com/icedo724/Loracle)
- [리포트](https://www.notion.so/miniminimin/Loracle-32afbcdaed28807faab9f5c891532ffd?source=copy_link)
