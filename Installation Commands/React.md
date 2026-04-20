# React Guide

## What is React?

React is a JavaScript library for building fast and interactive user interfaces, especially for single-page applications (SPAs). It is component-based, meaning you build reusable UI blocks and combine them to create pages.

Key points:
- Developed by Meta
- Uses components and props
- Uses a virtual DOM for efficient updates
- Commonly used with tools like Vite, React Router, and state libraries

## Prerequisites

Before creating a React project, make sure you have:
- Node.js 18+ installed
- npm (included with Node.js)
- VS Code or another editor
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
node --version
npm --version
```

## Create a React Project with Vite (Recommended)

Vite is the modern, fast way to start a React app.

### 1. Create project

```powershell
npm create vite@latest <project_name> -- --template react
```

### 2. Move into project folder

```powershell
cd <project_directory_name>
```

### 3. Install dependencies

```powershell
npm install
```

### 4. Start development server

```powershell
npm run dev
```

Open the local URL shown in terminal (usually):
- http://localhost:5173/

## Project Structure (Vite + React)

```text
my-react-app/
	node_modules/
	public/
	src/
		App.jsx
		main.jsx
		index.css
	index.html
	package.json
	vite.config.js
```

## Create Your First Custom Component

### 1. Create a new file: `src/components/Greeting.jsx`

```jsx
function Greeting({ name }) {
	return <h2>Hello, {name}!</h2>;
}

export default Greeting;
```

### 2. Use it in `src/App.jsx`

```jsx
import Greeting from './components/Greeting';

function App() {
	return (
		<>
			<h1>My React App</h1>
			<Greeting name="Developer" />
		</>
	);
}

export default App;
```

## Useful React/NPM Commands

```powershell
npm run dev
npm run build
npm run preview
npm run lint
```

## Build for Production

```powershell
npm run build
```

The production files will be generated in the `dist/` folder.

## Optional: Create React Project with TypeScript

```powershell
npm create vite@latest <project-name> -- --template react-ts
cd <project-name>
npm install
npm run dev
```

## Common Issues and Fixes

- `node` not found:
	- Install Node.js from the official website and restart terminal
- `npm install` fails:
	- Delete `node_modules` and `package-lock.json`, then run `npm install` again
- Port already in use:
	- Vite may choose another port automatically, or run:
		- `npm run dev -- --port 5174`

