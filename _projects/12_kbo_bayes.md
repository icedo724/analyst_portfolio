---
layout: page
title: "KBO 베이지안 타율·진출확률 추정"
description: "시즌 초 타율의 평균회귀를 베이지안 shrinkage로 보정 — 매일 자동 수집·갱신되는 추론 파이프라인"
img: assets/img/proj_kbo.png
importance: 1
category: 개인
tags: [Python, 베이지안, Beta-Binomial, Supabase, GitHub Actions, Next.js]
related_publications: false
links:
  - text: GitHub
    url: "https://github.com/icedo724/kbo-bayes"
    icon: "fab fa-github"
  - text: 대시보드
    url: "https://kbo-bayes.vercel.app"
    icon: "fa-solid fa-chart-bar"
---

## 배경 및 문제 정의

시즌 초 20타수 8안타(.400)인 선수가 진짜 4할 타자일 가능성은 낮다 — 대부분 평균으로 회귀한다. 그런데 "관측 타율을 그대로 쓰는" 베이스라인은 표본이 적을수록 과대·과소 추정이 심하다. **표본 크기를 반영해 '실력'을 추정**하는 것이 목표다.

## 데이터

- KBO 공식 기록실 수집 (`requests` + `pandas.read_html`, robots.txt 준수, Selenium 미사용)
- 전 구단 로스터 타자의 경기별 기록 → **시점별 누적 snapshot**으로 복원 (look-ahead 차단)
- 매일 **GitHub Actions** cron으로 자동 수집·갱신, **Supabase(Postgres)** 저장

## 모델 — Beta-Binomial 베이지안 shrinkage

각 타자: `H ~ Binomial(AB, θ)`, `θ ~ Beta(α, β)` → 사후 `θ | data ~ Beta(α+H, β+AB−H)`. 켤레 사전분포라 닫힌형 해가 나와 MCMC 없이 매일 가볍게 갱신한다. 사전분포는 리그 전체 타율 분포에서 empirical Bayes(method of moments)로 추정하며, 표본이 적을수록 리그 평균으로 강하게 수축한다.

{% include figure.liquid loading="eager" path="assets/img/chart_kbo_shrinkage.png" class="img-fluid rounded" caption="표본이 적은 선수(빨강)일수록 관측 타율이 리그 평균 쪽으로 강하게 보정된다" %}

## 정직한 검증

- **다년 walk-forward (2021–2025)**: 5개 시즌 × 6시점 = 30개 검증 지점 전부에서 베이지안이 베이스라인을 앞섬 (accuracy 금지, log loss·Brier 사용)
- **Calibration**: 예측-실제 평균절대오차 0.015 vs 베이스라인 0.030 — 베이스라인은 극단 구간을 과대·과소 예측
- **정직성**: MLE 사전분포는 시즌 초 소표본에서 발산(과수축) → 안정적인 method of moments 채택. 이 한계를 그대로 보고

{% include figure.liquid loading="eager" path="assets/img/chart_kbo_validation.png" class="img-fluid rounded" caption="5개 시즌 모두 베이지안(네이비)이 베이스라인보다 낮은 오차" %}

## 확장 & 운영

- 타율 외 **출루율(OBP)**로 확장(볼넷·사구 포함, 득점과의 상관이 더 높음)
- **가을야구 진출 확률**: 잔여 경기 몬테카를로 시뮬레이션, 2021–2025 다년 검증
- 오프라인(검증·동결) / 온라인(매일 예측) 물리적 분리, look-ahead 차단을 코드 구조로 강제
- **Next.js 포털 대시보드**(Vercel): 팀·선수별 추정, 시즌 궤적, 진출 확률을 매일 시각화

## 핵심 결과

단순 일회성 분석이 아니라 **매일 스스로 수집·추정·갱신하는 추론 시스템**을 end-to-end로 구축했다. 표본이 적을수록 강하게 보정되고(예: 5타수 .400 → .262), 표본이 쌓인 주전은 거의 보정되지 않으며, 그 우월성을 다년에 걸쳐 정직하게 검증했다.
