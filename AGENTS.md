<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

# AGENTS.md 프로젝트 지침

# 프로젝트 지침

## 프로젝트 목적

이 저장소는 Codex Community Hackathon 사전 연습용 프로젝트다.

목표는 짧은 시간 안에 작지만 실제로 동작하는 MVP를 구현하고 배포하는 것이다.

완벽한 구조보다 **작동하는 핵심 사용자 흐름, 빠른 검증, 안정적인 배포**를 우선한다.

## MVP

프로젝트명: AI Task Organizer

핵심 사용자 흐름:

1. 사용자가 자유롭게 텍스트를 입력한다.
2. OpenAI API가 입력을 실행 가능한 Task 3개로 변환한다.
3. 생성된 Task를 화면에 보여준다.
4. 사용자가 저장할 수 있다.
5. Task를 Supabase에 저장한다.

명시적인 요청이 없는 한 이 핵심 흐름 밖의 기능을 추가하지 않는다.

## 기술 스택

- Next.js
- TypeScript
- Tailwind CSS
- OpenAI API
- Supabase
- Vercel

## 개발 원칙

- 해커톤 속도와 단순성을 최우선으로 한다.
- 요구사항을 만족하는 가장 작은 구현을 선호한다.
- 불필요한 추상화와 계층을 만들지 않는다.
- 요청하지 않은 인증, 관리자, 설정 페이지 등을 추가하지 않는다.
- 가능하면 핵심 사용자 흐름을 한 페이지 안에서 유지한다.
- 기존 코드를 먼저 재사용한다.
- 명확한 이유 없이 새로운 라이브러리를 추가하지 않는다.
- 임의로 제품 범위를 확장하지 않는다.
- 새로운 기능보다 이미 구현된 핵심 흐름의 안정성을 우선한다.

## Codex 작업 방식

중요한 작업을 구현하기 전:

1. 관련 코드를 먼저 확인한다.
2. 필요한 경우 현재 설치된 Next.js 문서를 확인한다.
3. 현재 문제와 요구사항을 이해한다.
4. 구현 계획을 짧게 설명한다.
5. 요구사항을 만족하는 최소한의 구현을 수행한다.
6. 구현 결과를 직접 검증한다.

코드를 바로 수정하는 것보다 원인 분석이 필요한 문제라면 먼저 원인을 설명한다.

### 디버깅

오류가 발생하면:

1. 오류 메시지와 관련 코드를 확인한다.
2. 가장 가능성이 높은 원인을 찾는다.
3. 수정 범위를 최소화한다.
4. 수정 후 동일한 상황을 다시 검증한다.
5. 기존 정상 흐름이 깨지지 않았는지도 확인한다.

원인을 이해하지 못한 채 오류를 숨기거나 우회하지 않는다.

## Git 운영

해커톤 속도를 위해 `main` 브랜치 하나만 사용한다.

- 별도의 feature branch를 만들지 않는다.
- 명시적인 요청이 없는 한 PR을 만들지 않는다.
- GitHub Issue 생성은 필수가 아니다.
- 의미 있는 작업 단위로 커밋한다.
- 가능한 경우 Conventional Commit 형식을 사용한다.

커밋 예시:

- `feat: implement task generation`
- `feat: integrate OpenAI API`
- `feat: persist tasks with Supabase`
- `fix: handle invalid AI response`
- `docs: update build log`
- `chore: configure deployment`

작은 스타일 수정마다 별도 커밋을 만들 필요는 없다.

다른 팀원이 함께 작업하는 경우 현재 변경사항을 덮어쓰지 않도록 최신 코드를 확인한 뒤 작업한다.

## CodeRabbit 활용

CodeRabbit은 모든 변경마다 실행하지 않는다.

다음과 같은 주요 체크포인트에서만 사용한다.

1. 핵심 Happy Path가 처음 완성된 시점
2. 최종 제출 및 production 배포 전

리뷰에서는 우선적으로 다음을 확인한다.

- 실제 버그
- 보안 문제
- 데이터 손실 가능성
- 핵심 사용자 흐름을 막는 문제
- production 장애 가능성이 높은 문제

해커톤 중에는 단순 스타일, 취향 차이, 불필요한 리팩터링 제안은 우선순위를 낮춘다.

CodeRabbit의 제안을 무조건 적용하지 않는다.
현재 MVP 범위와 남은 시간을 고려해 사람이 적용 여부를 판단한다.

## 보안

- API Key와 secret을 클라이언트 코드에 노출하지 않는다.
- `.env.local`과 인증정보를 Git에 커밋하지 않는다.
- OpenAI API secret이 필요한 요청은 서버에서 수행한다.
- Supabase의 privileged credential은 서버에서만 사용한다.
- secret 값을 로그나 문서에 그대로 기록하지 않는다.

## 검증

의미 있는 코드 변경 후 필요한 검증을 수행한다.

작업 완료 전 최소한 다음을 확인한다.

- `npm run lint`
- `npm run build`

핵심 기능의 경우 코드 검사만으로 끝내지 않고 실제 사용자 흐름도 확인한다.

예:

`입력 → AI 처리 → 결과 표시 → 저장 → DB 확인`

자신의 변경으로 발생한 오류는 작업을 완료하기 전에 해결한다.

## BUILD_LOG 관리

`BUILD_LOG.md`는 Codex를 활용한 개발 과정과 팀의 판단을 기록하는 문서다.

모든 작은 수정마다 기록하지 않는다.

다음과 같은 의미 있는 사건이 발생했을 때 기록한다.

- 중요한 구현 방향 결정
- 핵심 기능 구현
- 사용자 또는 팀원 피드백을 반영한 변경
- 오류 발생과 복구
- Codex가 제안한 여러 방법 중 하나를 선택한 판단
- CodeRabbit 등 외부 검증 결과를 반영한 변경
- 배포 또는 production 문제 해결

각 기록에는 가능하면 다음을 포함한다.

- 목표 또는 문제
- Codex에 요청한 핵심 내용
- Codex의 제안 또는 수행 내용
- 사람이 내린 판단과 이유
- 결과
- 검증 방법
- 실패와 복구 과정이 있었다면 그 내용

실제로 발생하지 않은 내용은 기록하지 않는다.

Codex는 의미 있는 작업이 끝난 후 `BUILD_LOG.md`에 추가할 기록 초안을 제안하거나 작성할 수 있지만, 확인되지 않은 사실을 만들어내지 않는다.
