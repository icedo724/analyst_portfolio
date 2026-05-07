---
layout: page
title: 거래처 데이터 보강 및 등급 재조정
description: 직관 기반 거래처 등급을 정량 기준으로 전환 — 영업 우선순위 재편의 데이터 근거 마련
img: assets/img/proj_medi.svg
importance: 1
category: 실무
tags: [Python, SQL, 통계 검정, 카이제곱]
related_publications: false
---

기존 영업 조직이 직관에 의존하던 거래처 등급을 데이터로 재정의한 프로젝트.

**문제**
기존 등급 체계가 영업 인력의 경험·감에 의존하고 있어, 신규 인력의 우선순위 판단이 어려웠음.

**접근**
- 거래처 활동·매출·결제 행태 데이터를 통합
- 카이제곱 검정으로 등급 변수 간 통계적 유의성 검증
- 정량 기준으로 등급 재산정 → 영업 우선순위 재편

**도구**: Python · SQL · 카이제곱 검정

**결과물**
- [GitHub](https://github.com/icedo724/medi)
- [리포트](https://www.notion.so/miniminimin/2e0fbcdaed2880f1a37fe87f58603c1a?source=copy_link)
