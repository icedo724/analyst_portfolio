---
layout: page
title: 인게임 경제 시계열 분석: 이벤트 충격 분해 (로스트아크)
description: 재화 가격 시계열을 이벤트 단위로 분해하여 충격 패턴을 정량화 — 구조적 변동 요인 식별
img: assets/img/proj_loaquant.png
importance: 6
category: 개인
tags: [Python, 시계열, 인과추론, API]
related_publications: false
---

게임 내 재화 가격의 변동 원인을 이벤트 단위로 분해한 시계열 분석.

**접근**
- LostArk API로 재화 가격 시계열 수집
- 패치·이벤트 시점 마킹 후 가격 충격 분해
- 다음 충격의 예상 규모를 사전 가늠할 수 있는 판단 기준 도출

**도구**: Python · LostArk API · 시계열 분석

**결과물**
- [GitHub](https://github.com/icedo724/LoaQuant)
- [리포트](https://www.notion.so/miniminimin/318fbcdaed2880cd8de8dd88406d3564?source=copy_link)
- [대시보드](https://loaquant.streamlit.app/)
