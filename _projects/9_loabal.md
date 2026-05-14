---
layout: page
title: "LOABAL - 로스트아크 커뮤니티 감정분석"
description: "패치 전후 유저 감성 점수를 시계열로 시각화하여 유저 반응을 정량 측정"
img: ""
importance: 9
category: 개인
tags: [Python, Web Crawling, NLP, 감정분석]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/loabal"
    icon: "fab fa-github"
  - text: 리포트
    url: "https://www.notion.so/miniminimin/LOABAL-327fbcdaed28802fa544c1a4d081d356"
    icon: "fa-solid fa-file-lines"
---

## 배경 및 문제 정의

로스트아크 패치 전후 커뮤니티 반응을 감성 분석으로 정량화, 유저 감성 점수 시계열 시각화를 통해 "이번 패치에 유저들이 어떻게 반응했는가"를 수치로 제시한다.

## 분석 방법

- 커뮤니티 게시글 크롤링 및 텍스트 전처리
- 감성 분석 모델 적용 후 패치 전후 구간별 점수 산출
- 시계열 시각화로 패치 개입 효과 확인
