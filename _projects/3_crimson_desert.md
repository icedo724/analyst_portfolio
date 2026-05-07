---
layout: page
title: 붉은사막 Steam 리뷰 분석
description: 출시 후 6주 만족도 추세를 외부 AAA 출시작 2종과 정량 비교 — 핫픽스 시점 효과를 시계열 회귀로 입증
img: assets/img/proj_crimson.png
importance: 2
category: 게임
related_publications: false
---

게임 출시 후 6주차 시점 Steam 리뷰를 전수 분석해 만족도 추세·속성별 약점·패치 효과를 정량 측정.

**규모**: 본 IP 71k + 외부 벤치마크 376k = **총 446,884 리뷰**

**핵심 발견**
- 글로벌 만족도 1.01.00 정점 대비 -5.6%p 하락. 성능/최적화 -17.4%p가 주원인
- 회복 속도가 Elden Ring의 1.6~2배 — 1.00.03 핫픽스의 정량적 효과 입증
- 리뷰 좋아요 수 가중 시 -4.7%p 추가 하락 → 잠재 구매자 인상 위험 식별

**도구**: Python · Steam API · NLP · 시계열 회귀 · 통계 검정

**결과물**
- [GitHub](https://github.com/icedo724/crimson_desert_review)
- [리포트](https://www.notion.so/miniminimin/358fbcdaed28804e92f6c73ecc6fa899?source=copy_link)
