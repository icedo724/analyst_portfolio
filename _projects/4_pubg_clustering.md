---
layout: page
title: 배틀그라운드 유저 클러스터링
description: 유저 6,759명을 행동 패턴 4개 세그먼트로 분류 — 세그먼트별 독립 KPI 설계로 A/B 실험 정밀도 개선
img: assets/img/proj_pubg.svg
importance: 3
category: 게임
related_publications: false
---

단일 KPI 설계의 한계를 실증하고 세그먼트 기반 실험 프레임워크를 제안한 분석.

**문제**
전체 유저 평균 KPI는 세그먼트 간 행동 차이를 가려, A/B 실험 결과 해석에 노이즈 발생.

**접근**
- 6,759명 행동 데이터에 PCA·K-means 적용 → 4개 세그먼트 도출
- 세그먼트별 핵심 지표 분리 산정
- 층화 무작위 배정 기반 A/B 실험 프레임워크 설계

**도구**: Python · PUBG API · 클러스터링 · PCA · A/B 테스트

**결과물**
- [GitHub](https://github.com/icedo724/pubg_clustering)
- [리포트](https://www.notion.so/miniminimin/PUBG-344fbcdaed2880908668fb1db24185c1?source=copy_link)
