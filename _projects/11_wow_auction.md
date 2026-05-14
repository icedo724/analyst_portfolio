---
layout: page
title: "월드 오브 워크래프트 한밤 경제 분석"
description: "신규 확장팩 '한밤'에 따른 경매장 경제 변동 분석 및 로스트아크 분석 프레임워크의 이식 가능성 검증"
img: ""
importance: 11
category: 개인
tags: [Python, WoW API, 시계열, 통계 검정]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/WoW-Auction"
    icon: "fab fa-github"
  - text: 리포트
    url: "https://www.notion.so/miniminimin/32bfbcdaed288053bcfef33ce58e2d14"
    icon: "fa-solid fa-file-lines"
  - text: 대시보드
    url: "https://wowauction.streamlit.app/"
    icon: "fa-solid fa-chart-bar"
---

## 배경 및 문제 정의

신규 확장팩 '한밤' 출시에 따른 WoW 경매장 경제 변동을 분석하고, 로스트아크에서 구축한 시계열 분석 프레임워크가 다른 게임 경제에도 적용 가능한지 검증한다.

## 분석 방법

- WoW Auction House API로 아이템 가격·거래량 수집
- 확장팩 출시 전후 경제 지표 시계열 분석
- 로스트아크 분석 방법론 이식 및 결과 비교
