# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

개인 프로필 사이트 + ETF 분석 페이지로 구성된 정적 HTML 사이트입니다. 빌드 도구나 패키지 매니저 없이 브라우저에서 직접 열어 사용합니다.

## Pages

- `index.html` — 메인 프로필 페이지 (Home, About, Skills, Projects, Contact 섹션)
- `etf.html` — ETF 분석 페이지. Yahoo Finance v8 API에서 실시간 데이터를 가져옴

## ETF 데이터 로딩 구조

`etf.html`의 JavaScript는 두 계층으로 구성됩니다:

1. **정적 메타데이터** (`ETF_DATA` 객체) — 각 ETF의 전략, 특징, 이슈 등 하드코딩된 설명 데이터
2. **동적 데이터** (`fetchETFData`) — Yahoo Finance v8 Chart API에서 현재가·배당 이력을 fetch

### API 호출 방식

브라우저 CORS 제한으로 인해 프록시를 경유합니다:
- 1순위: `corsproxy.io/?url=`
- 2순위 fallback: `allorigins.win/get?url=` (응답이 `{ contents: "..." }` 형태로 래핑됨)

### 전일 종가 계산

`meta.chartPreviousClose`는 차트 범위 시작점(1년 전) 종가이므로 사용 금지.
전일 종가는 `result.indicators.quote[0].close` 배열의 마지막에서 두 번째 값을 사용합니다.

## Styling

Tailwind CSS를 CDN으로 로드합니다 (`https://cdn.tailwindcss.com`). 별도 설정 파일 없음.
색상 테마: 검정 배경 + 퍼플 계열 포인트 (`purple-400` ~ `purple-600`).
