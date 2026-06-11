# Domaksaramu Tech Blog

Notion을 CMS로 쓰는 개인 기술 블로그입니다.  
Next.js, `react-notion-x`, Vercel을 기반으로 동작하며, 현재 공개 주소는 [domaksaramu.vercel.app](https://domaksaramu.vercel.app) 입니다.

## Stack

- Next.js 14
- React 18
- TypeScript
- Notion API via `react-notion-x`
- Vercel
- pnpm

## Project Config

사이트 기본 설정은 [site.config.ts](/Users/jewon945/Documents/myVercelNotionBlog/site.config.ts:1) 에 있습니다.

현재 주요 설정:

- 사이트 이름: `Domaksaramu Tech Blog`
- 도메인: `domaksaramu.vercel.app`
- 언어: `ko-KR`
- Notion 루트 페이지 ID: `NOTION_PAGE_ID` 환경 변수 또는 `site.config.ts`의 기본값 사용
- 이미지 프리뷰: 활성화
- Redis 캐시: 비활성화

## Local Development

권장 환경:

- Node.js `24.x`
- pnpm `9.15.0`

설치 및 실행:

```bash
pnpm install
pnpm dev
```

기본 개발 서버 주소:

```bash
http://localhost:3000
```

## Available Scripts

```bash
pnpm dev
pnpm build
pnpm start
pnpm test:lint
pnpm exec tsc --noEmit
```

`pnpm build`는 프로덕션 번들을 생성합니다.  
배포 전에는 `pnpm test:lint`와 `pnpm exec tsc --noEmit`로 기본 검증을 하는 것을 권장합니다.

## Vercel Deployment

이 프로젝트는 GitHub 연동으로 Vercel에 배포합니다.

배포 시 확인할 점:

- Vercel 프로젝트의 Node.js 버전은 `24.x`
- Deployment Protection이 켜져 있으면 OG 이미지나 일부 공개 접근이 깨질 수 있음
- 루트 Notion 페이지는 반드시 공개 상태여야 함

현재 코드에서는 중첩된 Notion 하위 페이지 라우팅을 위해 사이트맵 탐색 깊이를 늘려둔 상태입니다. 깊은 하위 문서가 열리지 않으면 [lib/get-site-map.ts](/Users/jewon945/Documents/myVercelNotionBlog/lib/get-site-map.ts:39)의 `maxDepth` 설정을 먼저 확인하면 됩니다.

## Content Structure

이 블로그는 Notion 페이지 구조를 그대로 가져오되, 사람이 읽기 쉬운 slug를 자동 생성합니다.

- 루트 페이지 아래 문서와 하위 문서들을 정적으로 수집
- 공개된 페이지(`Public` 속성 기준)만 URL 맵에 포함
- 필요하면 `pageUrlOverrides`로 특정 경로를 수동 지정 가능

관련 코드:

- [pages/[pageId].tsx](/Users/jewon945/Documents/myVercelNotionBlog/pages/%5BpageId%5D.tsx:1)
- [lib/resolve-notion-page.ts](/Users/jewon945/Documents/myVercelNotionBlog/lib/resolve-notion-page.ts:1)
- [lib/get-site-map.ts](/Users/jewon945/Documents/myVercelNotionBlog/lib/get-site-map.ts:1)
- [lib/map-page-url.ts](/Users/jewon945/Documents/myVercelNotionBlog/lib/map-page-url.ts:1)

## Notes

- README에는 개인정보성 연락처 정보는 넣지 않았습니다.
- 현재 저장소는 원본 스타터킷에서 개인 블로그용으로 커스터마이즈된 상태입니다.
