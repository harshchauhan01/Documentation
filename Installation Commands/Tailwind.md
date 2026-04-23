# Tailwind CSS Guide

## What is Tailwind CSS?

Tailwind CSS is a utility-first CSS framework for building modern UI quickly by applying small, composable classes directly in your markup.

Key points:
- Utility-first approach (no large custom CSS files required)
- Fast prototyping and consistent design systems
- Works with React, Next.js, Vue, plain HTML, and more

## Prerequisites

Before setting up Tailwind CSS, make sure you have:
- Node.js 18+ installed
- npm (included with Node.js)
- A frontend project (React/Vite, Next.js, etc.)
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
node --version
npm --version
```

## Setup Tailwind CSS in React (Vite)

### 1. Create a React app (if you do not already have one)

```powershell
npm create vite@latest <project_name> -- --template react
cd <project_name>
npm install
```

### 2. Install Tailwind CSS (v4)

```powershell
npm install tailwindcss @tailwindcss/vite
```

### 3. Update `vite.config.js`

```js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
	plugins: [react(), tailwindcss()],
});
```

### 4. Import Tailwind in your CSS

In `src/index.css`, keep this line:

```css
@import "tailwindcss";
```

### 5. Start dev server

```powershell
npm run dev
```

## Setup Tailwind CSS in Next.js (App Router)

### 1. Create a Next.js app (if you do not already have one)

```powershell
npx create-next-app@latest <project_name>
cd <project_name>
```

### 2. Install Tailwind CSS (v4)

```powershell
npm install tailwindcss @tailwindcss/postcss postcss
```

### 3. Configure PostCSS

Create or update `postcss.config.mjs`:

```js
export default {
	plugins: {
		'@tailwindcss/postcss': {},
	},
};
```

### 4. Import Tailwind in global CSS

In `src/app/globals.css`, keep this line:

```css
@import "tailwindcss";
```

### 5. Start dev server

```powershell
npm run dev
```

Open in browser:
- http://localhost:3000/

## Test Tailwind Quickly

Use classes in a component/page to confirm Tailwind is working:

```jsx
export default function App() {
	return (
		<div className="min-h-screen bg-slate-100 flex items-center justify-center">
			<h1 className="text-3xl font-bold text-blue-600">Tailwind is working!</h1>
		</div>
	);
}
```

If styles apply, setup is complete.

## Useful Commands

```powershell
npm run dev
npm run build
npm run lint
```

## Optional: Tailwind CSS v3 Setup (Older Projects)

If your project still uses Tailwind v3 style setup:

```powershell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Then configure `tailwind.config.js` `content` paths and add the Tailwind directives in your CSS:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Common Issues and Fixes

- Classes not applying:
	- Make sure your main CSS file includes `@import "tailwindcss";` (v4) or Tailwind directives (v3)
- Dev server still showing old styles:
	- Stop and restart dev server
- Build errors after install:
	- Delete `node_modules` and lock file, then run `npm install` again
