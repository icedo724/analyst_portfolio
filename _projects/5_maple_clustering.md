---
layout: page
title: 메이플스토리 유저 행동 클러스터링
description: 활동·성장 패턴 기반 군집화 → 클러스터별 이탈 시점·쇼케이스 반응 차이를 생존 분석으로 검증
img: assets/img/proj_maple_cluster.svg
importance: 4
category: 게임
tags: [Python, 클러스터링, 생존 분석]
related_publications: false
---

유저 세그먼트별 이탈 패턴 차이를 통계로 검증한 분석.

**접근**
- Nexon API 실데이터로 활동 빈도·성장 효율 변수 구성
- 클러스터링으로 유저 군집 분리
- 생존 분석 (Kaplan-Meier·Log-rank)으로 클러스터별 이탈 시점 차이 검증
- 쇼케이스(이벤트) 반응 차이도 클러스터별로 분리 측정

**도구**: Python · Nexon API · 클러스터링 · 생존 분석

**결과물**
- [GitHub](https://github.com/icedo724/Maplestory_Analysis)
- [리포트](https://www.notion.so/miniminimin/346fbcdaed2880209e39ff1b490e34e5?source=copy_link)
- [대시보드](https://maple-user-clustering.streamlit.app/)
