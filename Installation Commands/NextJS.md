# Next.js Guide

## What is Next.js?

Next.js is a React framework for building production-ready web applications. It provides routing, server-side rendering, static site generation, API routes, and performance optimizations out of the box.

Key points:
- Built on top of React
- Supports server rendering and static generation
- Includes file-based routing
- Great for SEO-friendly and full-stack React apps

## Prerequisites

Before creating a Next.js project, make sure you have:
- Node.js 18.18+ installed (or newer LTS)
- npm (included with Node.js)
- VS Code or another editor
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
node --version
npm --version
```

## Create a Next.js Project (Step by Step)

### 1. Create project using the official starter

```powershell
npx create-next-app@latest <project_name>
```

This command will ask a few setup questions (TypeScript, ESLint, App Router, etc.).

### 2. Move into project folder

```powershell
cd <project_name>
```

### 3. Start the development server

```powershell
npm run dev
```

Open in browser:
- http://localhost:3000/

## Typical Project Structure

```text
my-next-app/
	node_modules/
	public/
	src/
		app/
			layout.js
			page.js
	package.json
	next.config.js
```

## Useful Next.js Commands

```powershell
npm run dev
npm run build
npm run start
npm run lint
```

## Add a Simple API Route (App Router)

Create file: `src/app/api/hello/route.js`

```js
import { NextResponse } from 'next/server';

export async function GET() {
	return NextResponse.json({ message: 'Hello from Next.js API route!' });
}
```

Run server and visit:
- http://localhost:3000/api/hello

## Build for Production

```powershell
npm run build
npm run start
```

## Common Issues and Fixes

- `npx` not found:
	- Reinstall Node.js and reopen terminal
- Dependency install problems:
	- Run `npm cache clean --force` and then `npm install`
- Port 3000 already in use:
	- Run dev server on another port: `npm run dev -- -p 3001`
