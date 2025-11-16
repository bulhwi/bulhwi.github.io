# CLAUDE.md

> Claude Code를 위한 프로젝트 가이드 문서

## 프로젝트 개요

**bulhwi.github.io**는 Next.js와 Tailwind CSS 기반의 개인 기술 블로그입니다.

- **템플릿**: [Tailwind Nextjs Starter Blog](https://github.com/timlrx/tailwind-nextjs-starter-blog)
- **배포**: GitHub Pages (Static Export)
- **주제**: 프론트엔드, TypeScript, Git, DevOps 등 개발 관련 기술 문서

## 기술 스택

### Core

- **Next.js** 12.1.4
- **React** 17.0.2 → Preact (프로덕션)
- **Tailwind CSS** 3.0.23

### Content

- **mdx-bundler** - MDX 처리
- **gray-matter** - Frontmatter 파싱
- **rehype-prism-plus** - 코드 하이라이팅
- **rehype-katex** - 수식 렌더링
- **remark-gfm** - GitHub Flavored Markdown

### Build & Deploy

- **Static Export** - `next build && next export`
- **Akamai Image Loader** - 정적 호스팅 환경용

## 프로젝트 구조

```
.
├── components/        # React 컴포넌트
├── css/              # 전역 스타일 (Tailwind, Prism)
├── data/             # 블로그 컨텐츠 및 설정
│   ├── blog/
│   │   ├── doc/      # 주요 기술 문서 (공개)
│   │   ├── closed/   # 비공개/보관 문서
│   │   └── nested-route/
│   ├── authors/      # 작성자 정보
│   ├── siteMetadata.js
│   ├── headerNavLinks.js
│   └── projectsData.js
├── layouts/          # 페이지 레이아웃 템플릿
├── lib/              # 유틸리티 함수
├── pages/            # Next.js 페이지
│   ├── api/          # API 라우트
│   ├── blog/         # 블로그 동적 라우팅
│   └── tags/         # 태그별 필터링
├── public/           # 정적 파일
└── scripts/          # 빌드/유틸 스크립트
```

## 주요 설정 파일

### `data/siteMetadata.js`

사이트 전반의 메타데이터 관리:

- 사이트 제목, 설명, URL
- 소셜 링크 (GitHub, Twitter 등)
- Analytics 설정
- 댓글 시스템 (Giscus)
- Newsletter 설정

### `next.config.js`

Next.js 설정:

- 이미지 로더: Akamai (정적 호스팅용)
- 보안 헤더: CSP, HSTS, X-Frame-Options 등
- Preact 교체 (프로덕션 빌드 경량화)
- SVG 처리: @svgr/webpack

### `tailwind.config.js`

Tailwind CSS 커스터마이징:

- 색상 테마
- 타이포그래피 플러그인
- Forms 플러그인

## 블로그 포스트 작성 가이드

### Frontmatter 필드

```yaml
---
title: '포스트 제목' # 필수
date: 2025-06-22T15:46 # 필수
lastmod: '2025-06-22' # 선택
tags: ['frontend', 'typescript'] # 필수 (빈 배열 가능)
draft: false # 선택 (true면 비공개)
summary: '짧은 요약' # 선택 (목록에 표시)
layout: PostSimple # 선택 (기본값: PostLayout)
images: ['/static/images/...'] # 선택 (소셜 미리보기)
authors: ['default'] # 선택 (기본값: default)
canonicalUrl: https://... # 선택 (SEO용)
---
```

### 파일 위치

- **공개 문서**: `data/blog/doc/*.mdx`
- **비공개**: `data/blog/closed/*.mdx`
- **다단계 시리즈**: `data/blog/nested-route/*.mdx`

### 새 포스트 생성

```bash
node ./scripts/compose.js
```

→ 대화형 프롬프트로 Frontmatter가 미리 채워진 파일 생성

## 개발 명령어

```bash
# 개발 서버 (hot reload + watch)
npm start

# 개발 서버 (일반)
npm run dev

# 프로덕션 빌드 + Static Export + Sitemap 생성
npm run build

# 프로덕션 서버 (로컬 테스트)
npm run serve

# 번들 분석
npm run analyze

# Lint + 자동 수정
npm run lint
```

## 배포 프로세스

1. **빌드**: `npm run build`

   - Next.js 빌드
   - Static HTML Export
   - Sitemap 생성

2. **출력**: `out/` 디렉토리에 정적 파일 생성

3. **GitHub Pages**: `out/` 디렉토리를 `gh-pages` 브랜치에 푸시

## 주요 기능

### 1. 이미지 최적화

- Static Export 환경이므로 Akamai 로더 사용
- `next/image` 컴포넌트 활용

### 2. 코드 하이라이팅

- `rehype-prism-plus` 사용
- 라인 넘버, 라인 하이라이팅 지원
- 테마: `css/prism.css`에서 커스터마이징

### 3. 수식 표현

- KaTeX로 LaTeX 수식 렌더링
- 인라인/블록 수식 모두 지원

### 4. 댓글 시스템

- Giscus (GitHub Discussions 기반)
- `.env` 파일에 설정 필요:
  - `NEXT_PUBLIC_GISCUS_REPO`
  - `NEXT_PUBLIC_GISCUS_REPOSITORY_ID`
  - `NEXT_PUBLIC_GISCUS_CATEGORY`
  - `NEXT_PUBLIC_GISCUS_CATEGORY_ID`

### 5. 보안

- Content Security Policy 설정
- HSTS, X-Frame-Options 등 보안 헤더 적용

## 커스터마이징 포인트

### 네비게이션 변경

`data/headerNavLinks.js` 수정

### 프로젝트 페이지

`data/projectsData.js`에 프로젝트 추가

### 작성자 정보

`data/authors/default.md` 수정 또는 새 작성자 추가

### 스타일링

- `tailwind.config.js` - 색상, 폰트 등
- `css/tailwind.css` - 전역 스타일
- `css/prism.css` - 코드 블록 테마

## 주의사항

### Static Export 제약

- API Routes는 동적 실행 불가
- Newsletter 기능은 외부 API 서비스 필요
- `next/image`는 Akamai 로더 사용

### 환경 변수

`.env.example` 참고하여 `.env` 파일 생성:

- Giscus 설정
- Analytics ID
- Newsletter API 키

### Git Hooks

- Husky로 pre-commit 훅 설정
- ESLint + Prettier 자동 실행
- `lint-staged`로 변경된 파일만 검사

## 블로그 컨텐츠 현황

### 주요 주제

1. **TypeScript** - Effective TypeScript 시리즈
2. **Git** - reflog, rebase, merge 가이드
3. **프론트엔드** - 브라우저 렌더링, CSS 최적화
4. **Java** - Optional, Stream, Lambda
5. **DevOps** - Docker, Kubernetes
6. **JavaScript** - Clean Code 패턴

### 최근 작업

- Effective TypeScript Item 7 작성 중
- 부제목 및 메타데이터 업데이트

## 문제 해결

### 빌드 에러

1. `node_modules` 재설치: `rm -rf node_modules && npm install`
2. `.next` 캐시 삭제: `rm -rf .next`
3. Node 버전 확인 (권장: Node 14+)

### 이미지 최적화 이슈

- Static Export 환경이므로 `next/image`의 일부 기능 제한
- 필요시 `<img>` 태그로 대체 가능

### 배포 후 404 에러

- GitHub Pages의 경로 설정 확인
- `next.config.js`의 `basePath` 확인

## 참고 자료

- [Next.js 공식 문서](https://nextjs.org/docs)
- [Tailwind CSS 문서](https://tailwindcss.com/docs)
- [MDX 문서](https://mdxjs.com/)
- [템플릿 저장소](https://github.com/timlrx/tailwind-nextjs-starter-blog)

---

**Last Updated**: 2025-11-16
