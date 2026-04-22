# MongoDB Guide

## What is MongoDB?

MongoDB is a NoSQL database that stores data in flexible, JSON-like documents (BSON). It is a good choice for applications that need fast iteration and flexible schemas.

Key points:
- Document-oriented database
- Schema-flexible collections
- Good horizontal scalability
- Commonly used with Node.js and modern web apps

## Prerequisites

Before installing MongoDB, make sure you have:
- Windows 10/11
- Administrator access
- PowerShell terminal
- VS Code or another editor

## Install MongoDB Community Edition on Windows (Step by Step)

### 1. Download installer

Go to the official MongoDB Community Server download page and download the MSI installer for Windows.

### 2. Run installer

- Start the MSI installer
- Choose Complete setup
- Keep Install MongoDB as a Service enabled
- Optionally install MongoDB Compass (GUI)

### 3. Verify installation

Open a new PowerShell terminal and run:

```powershell
mongod --version
mongosh --version
```

If `mongosh` is not found, install MongoDB Shell separately from the official MongoDB website.

## Start and Stop MongoDB Service

If installed as a Windows service:

```powershell
Get-Service MongoDB
Start-Service MongoDB
Stop-Service MongoDB
Restart-Service MongoDB
```

## Connect to MongoDB

Run:

```powershell
mongosh
```

Common shell commands:

```javascript
show dbs
use app_db
db.createCollection('users')
db.users.insertOne({ name: 'Alice', email: 'alice@example.com' })
db.users.find()
```

## Typical Project Structure (Node.js + MongoDB)

```text
my-app/
	src/
		config/
			db.js
		models/
	package.json
	.env
```

## Use MongoDB in Node.js (Quick Example)

Install driver:

```powershell
npm install mongodb
```

Example `db.js`:

```js
const { MongoClient } = require('mongodb');

const uri = process.env.MONGODB_URI || 'mongodb://127.0.0.1:27017';
const client = new MongoClient(uri);

async function connectDb() {
	await client.connect();
	return client.db('app_db');
}

module.exports = { connectDb };
```

## Useful MongoDB Commands

```powershell
mongod --version
mongosh
mongosh "mongodb://127.0.0.1:27017"
```

Inside `mongosh`:

```javascript
show dbs
show collections
use app_db
db.users.find()
db.users.updateOne({ name: 'Alice' }, { $set: { active: true } })
db.users.deleteOne({ name: 'Alice' })
```

## Common Issues and Fixes

- `mongosh` or `mongod` not found:
	- Reopen terminal and check PATH, or reinstall MongoDB Shell
- Service does not start:
	- Check Windows Services and MongoDB logs
- Port 27017 already in use:
	- Stop conflicting process or configure MongoDB to use another port
