# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This repository is a collection of small, standalone browser tools and reports (no shared app, no backend). Each deliverable is typically a single self-contained `.html` file with inline CSS/JS. Examples: `hello.html`, `지점별_실적_리포트.html`, `증권사_경쟁분석_리포트.html`, `관심종목_대시보드.html`.

## 기술스택

- **순수 HTML/CSS/JS만 사용한다.** 프레임워크·번들러·npm 패키지를 추가하지 않는다. 산출물은 항상 단일 `.html` 파일로 열면 바로 동작해야 한다.
- CSS는 파일 상단 `<style>`에 인라인으로 작성하고, 라이트/다크 테마는 CSS custom property로 분리한다(`--surface-1`, `--text-primary` 등). `prefers-color-scheme`과 `data-theme` 속성 토글을 함께 지원한다.
- JS는 `<script>`에 인라인으로 작성하고, IIFE + `"use strict"`로 감싸 전역 스코프를 오염시키지 않는다. 외부 CDN/라이브러리는 쓰지 않는다(차트도 손으로 그린 SVG 사용).
- 클라이언트 쪽 상태 저장이 필요하면 `localStorage`를 쓴다. 로그인/백엔드가 없는 도구는 새로고침 후에도 데이터가 유지되는지를 완료 기준에 포함한다.
- 차트/시각화가 필요한 작업은 `dataviz` 스킬의 절차(색상 검증, 마크 스펙, 라이트/다크 모드, 접근성 체크)를 따른다.

## 작업 규칙

- 새 도구를 만들기 전, 요구사항이 조금이라도 복잡하면 `PRD.md`를 먼저 작성하고 사용자 확인을 받은 뒤 구현한다(핵심기능/화면구성/제외범위/검증기준/가정 구조를 따른다).
- 파일명은 한글 설명형으로 짓고 기존 파일들과 톤을 맞춘다(예: `지점별_실적_리포트.html`, `관심종목_대시보드.html`).
- 리서치가 필요한 작업(경쟁사 분석 등)은 1차 공개 출처만 사용하고, 모든 수치·주장에 출처 링크를 남기며, 확인되지 않은 내용은 "미확인"으로 표시한다.
- 반복해서 쓸 만한 절차는 `.claude/skills/`에 스킬로 등록해 재사용한다(예: `회의록정리` 스킬).

## Development

There is no build, lint, or test tooling configured. To verify a change, open the `.html` file directly in a browser (e.g. `start 관심종목_대시보드.html` on Windows). This repository is not a git repository — there is no version history to rely on, so check file contents directly when in doubt about existing state.
