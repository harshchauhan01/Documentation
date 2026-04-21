# Express.js Guide

## What is Express.js?

Express.js is a minimal and flexible web framework for Node.js used to build APIs and web servers quickly.

Key points:
- Built on top of Node.js
- Simple routing and middleware system
- Common choice for REST APIs
- Large ecosystem and community support

## Prerequisites

Before creating an Express.js project, make sure you have:
- Node.js LTS installed
- npm available
- VS Code or another editor
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
node --version
npm --version
```

## Create an Express.js Project (Step by Step)

### 1. Create and open a project folder

```powershell
mkdir express_project
cd express_project
```

### 2. Initialize npm

```powershell
npm init -y
```

### 3. Install Express

```powershell
npm install express
```

### 4. Create server file

```powershell
New-Item server.js -ItemType File
```

Add this code to `server.js`:

```js
const express = require('express');
const app = express();

const PORT = 3000;

app.get('/', (req, res) => {
	res.send('Hello from Express.js!');
});

app.listen(PORT, () => {
	console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 5. Run the server

```powershell
node server.js
```

Open in browser:
- http://localhost:3000/

## Typical Project Structure

```text
express_project/
	node_modules/
	server.js
	package.json
	package-lock.json
```

## Useful Express and npm Commands

```powershell
node server.js
npm install express
npm install -D nodemon
npx nodemon server.js
```

## Optional: Add Dev Script with Nodemon

Install nodemon:

```powershell
npm install -D nodemon
```

In `package.json`, add scripts:

```json
"scripts": {
	"start": "node server.js",
	"dev": "nodemon server.js"
}
```

Run in development mode:

```powershell
npm run dev
```

## Common Issues and Fixes

- `Cannot find module 'express'`:
	- Install dependencies again with `npm install`
- Port already in use:
	- Change port in code or stop the process using that port
- Server not restarting automatically:
	- Use `nodemon` and run with `npm run dev`
