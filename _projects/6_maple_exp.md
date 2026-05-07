---
layout: page
title: 대규모 실데이터 기반 이벤트 효과 정량 측정 (메이플스토리 96k)
description: 285Lv 이상 유저 96,000명 데이터로 신규 지역·이벤트의 성장 지표 영향을 통계 검정으로 측정
img: assets/img/proj_maple_exp.svg
importance: 5
category: 게임
tags: [Python, Nexon API, 통계 검정, 시계열]
related_publications: false
---

대규모 유저 데이터로 게임 내 이벤트의 영향력을 통계 검정으로 측정한 분석.

**접근**
- Nexon API로 285레벨 이상 활성 유저 96,000명 실데이터 수집
- 신규 지역 공개 전후 경험치 획득량 변화 측정
- 썬데이 메이플(주말 이벤트)의 경험치 영향 통계 검정

**도구**: Python · Nexon API · 통계 검정

**결과물**
- [GitHub](https://github.com/icedo724/Maplestory_Analysis)
- [리포트](https://www.notion.so/miniminimin/32afbcdaed288075a929eb7f533361b0?source=copy_link)
- [대시보드](https://maple-exp.streamlit.app/)
