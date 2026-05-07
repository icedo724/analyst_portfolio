---
layout: page
title: "JobSonar — 채용공고 기술스택 빈도 분석"
description: 채용공고 자동 수집부터 직무·기술 스택 빈도 시각화까지 — 취업 시장 트렌드 한 페이지 집약
img: assets/img/proj_jobsonar.svg
importance: 7
category: 개인
tags: [Python, Selenium, Streamlit, NLP]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/JobSonar"
    icon: "fab fa-github"
  - text: 대시보드
    url: "https://huggingface.co/spaces/mininiming/jobsonar"
    icon: "fa-solid fa-chart-bar"
---

데이터 직군 채용 시장의 트렌드를 한 화면에 집약한 대시보드.

**문제**
취업 준비자가 직무별 요구 스킬·근무 조건을 종합적으로 파악할 단일 채널이 부재.

**접근**
- 주요 채용 사이트 자동 크롤링
- SQLite DB 설계 → SQL 집계 쿼리
- Dash 기반 대시보드 (직무·기술 스택·근무 조건 필터)

**도구**: Python · SQL · SQLite · Web Crawling · Dash
