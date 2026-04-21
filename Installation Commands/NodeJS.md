# Node.js Guide

## What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 engine. It allows you to run JavaScript on the server side and build backend services, APIs, CLIs, and tooling.

Key points:
- Runs JavaScript outside the browser
- Event-driven and non-blocking I/O
- Widely used for APIs and real-time apps
- Includes npm for package management

## Prerequisites

Before starting with Node.js, make sure you have:
- Node.js LTS installed
- npm (included with Node.js)
- VS Code or another editor
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
node --version
npm --version
```

## Create a Basic Node.js Project (Step by Step)

### 1. Create and open a project folder

```powershell
mkdir node_project
cd node_project
```

### 2. Initialize npm

```powershell
npm init -y
```

### 3. Create an entry file

```powershell
New-Item index.js -ItemType File
```

Add this code to `index.js`:

```js
console.log('Hello from Node.js!');
```

### 4. Run the app

```powershell
node index.js
```

## Typical Project Structure

```text
node_project/
	node_modules/
	index.js
	package.json
	package-lock.json
```

## Useful Node.js and npm Commands

```powershell
node index.js
npm init -y
npm install <package_name>
npm uninstall <package_name>
npm update
npm run <script_name>
```

## Add a Start Script

In `package.json`, update scripts:

```json
"scripts": {
	"start": "node index.js"
}
```

Then run:

```powershell
npm start
```

## Common Issues and Fixes

- `node` not found:
	- Reinstall Node.js and ensure PATH is configured
- `npm` permission errors:
	- Run terminal as administrator (if needed) and retry
- Package install fails:
	- Delete `node_modules` and `package-lock.json`, then run `npm install`
