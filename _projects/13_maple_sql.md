---
layout: page
title: "메이플 유저 활동 분석 — SQL 에디션"
description: "직접 수집한 1,200만 행 유저 활동 패널을 MySQL로 정규화 — 코호트 리텐션·휴면 복귀·이탈을 순수 SQL로 분석, 인덱스 튜닝 실측 12.05s→1.61s"
img: assets/img/proj_maple_exp.svg
importance: 4
category: 개인
tags: [SQL, MySQL, 윈도우 함수, 코호트 분석]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/maple-user-analytics-sql"
    icon: "fab fa-github"
---

넥슨 오픈API로 수집한 **유저 99,521명 × 126일 패널(11,979,122행)** 을 MySQL 8.0에 정규화 적재하고, 프로덕트 분석의 핵심 질문들을 순수 SQL로 답했다. [경험치 영향 통계 분석](/analyst_portfolio/projects/6_maple_exp/)과 같은 데이터, 다른 관점이다.

## 스키마와 모델링 결정

`users` / `daily_activity`(PK: user_id, activity_date) / `events` / `sunday_events` 4테이블. 원본 wide CSV의 **NULL(관측 실패)과 0(활동 없음)을 구분**해 관측된 행만 적재 — 그 결과 1/15 수집 장애가 행의 부재로 드러나고, 인접일 DAU 스파이크를 수집 아티팩트로 식별할 수 있었다.

## 분석 질문 6개 (쿼리당 1기법)

| 질문 | 기법 | 핵심 결과 |
|---|---|---|
| DAU/롤링 WAU/스티키니스 | 비등가 자기조인, `AVG() OVER` | 스티키니스 72~79% — 매일 접속하는 코어 집단 |
| 진입 코호트 리텐션 | 조건부 집계 피벗, 절단 처리 | W12 잔존 90%+, 고정 패널 구조를 데이터로 역추적 |
| 휴면 복귀 | `LAG()` 활동 갭 | 헤이스트의 휴면 복귀 효과 없음 — 피크는 이벤트 직전 주 |
| 이탈·잔존 곡선 | 우측 절단 처리 | 레벨이 높을수록 이탈률 감소 (4.5%→3.5%) |
| 세그먼트×요일, 분포 | `WITH ROLLUP`, `PERCENT_RANK`, `NTILE` | 전 구간 일요일 최대, P99/P50 = 16배 꼬리 |
| 성능 튜닝 | `EXPLAIN ANALYZE` | 풀스캔 12.05s → 커버링 인덱스 **1.61s (7.5배)** |

## 회고

윈도우 함수·코호트 쿼리를 "아는 것"과 1,200만 행에서 "돌아가게 만드는 것"의 차이를 체감했다. PK 설계가 쿼리 패턴과 어긋날 때의 비용, InnoDB 보조 인덱스의 커버링 특성, `LOAD DATA` 권한 제약 시의 적재 전략까지 — 전 과정과 실측 수치를 [README](https://github.com/icedo724/maple-user-analytics-sql)에 기록했다.
