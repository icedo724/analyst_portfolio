---
layout: page
title: "리그오브레전드 상위 플레이어 메타 대시보드"
description: "마스터 이상 실데이터 기반 챔피언 픽률·승률 사분면 분류로 메타 통계 서비스 구현"
img: ""
importance: 10
category: 개인
tags: [Python, Riot API, 통계 검정, Streamlit]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/LoL-DashBoard"
    icon: "fab fa-github"
  - text: 대시보드
    url: "https://lolhighplayer.streamlit.app/"
    icon: "fa-solid fa-chart-bar"
---

## 배경 및 문제 정의

마스터 이상 고티어 플레이어의 실데이터를 기반으로 챔피언별 픽률·승률을 사분면으로 분류하여, 메타 통계 서비스와 유사한 구조의 대시보드를 직접 구현한다.

## 분석 방법

- Riot API로 마스터 이상 매치 데이터 수집
- 챔피언별 픽률·승률 집계 및 사분면 분류
- Streamlit 대시보드로 실시간 시각화 제공
