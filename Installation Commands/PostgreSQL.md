# PostgreSQL Guide

## What is PostgreSQL?

PostgreSQL is an open-source relational database system known for reliability, standards compliance, and advanced SQL features.

Key points:
- Relational database (SQL)
- Strong ACID compliance
- Supports indexes, constraints, JSON, and extensions
- Commonly used in production web applications

## Prerequisites

Before installing PostgreSQL, make sure you have:
- Windows 10/11
- Administrator access
- PowerShell terminal
- VS Code or another editor

## Install PostgreSQL on Windows (Step by Step)

### 1. Download installer

Download the Windows installer from the official PostgreSQL website (EDB installer).

### 2. Run installer

During setup, configure:
- Installation directory
- Superuser password for `postgres`
- Port (default: `5432`)
- Locale (default is usually fine)

### 3. Verify installation

Open PowerShell and run:

```powershell
psql --version
```

If command is not found, add PostgreSQL `bin` directory to PATH or reopen terminal.

## Connect to PostgreSQL

### Option 1: Using SQL Shell (`psql`)

```powershell
psql -U postgres -h localhost -p 5432
```

### Option 2: Connect to a specific database

```powershell
psql -U postgres -d app_db -h localhost -p 5432
```

## Basic SQL Setup (Step by Step)

Inside `psql`:

```sql
CREATE DATABASE app_db;
\c app_db

CREATE TABLE users (
	id SERIAL PRIMARY KEY,
	name VARCHAR(100) NOT NULL,
	email VARCHAR(150) UNIQUE NOT NULL,
	created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

INSERT INTO users (name, email)
VALUES ('Alice', 'alice@example.com');

SELECT * FROM users;
```

## Useful PostgreSQL Commands

PowerShell:

```powershell
psql --version
psql -U postgres -h localhost -p 5432
```

Inside `psql`:

```sql
\l
\c app_db
\dt
\d users
SELECT * FROM users;
\q
```

## Typical Project Structure (Node.js + PostgreSQL)

```text
my-app/
	src/
		config/
			db.js
		migrations/
	package.json
	.env
```

## Use PostgreSQL in Node.js (Quick Example)

Install package:

```powershell
npm install pg
```

Example `db.js`:

```js
const { Pool } = require('pg');

const pool = new Pool({
	host: process.env.PGHOST || 'localhost',
	port: Number(process.env.PGPORT || 5432),
	user: process.env.PGUSER || 'postgres',
	password: process.env.PGPASSWORD,
	database: process.env.PGDATABASE || 'app_db',
});

module.exports = { pool };
```

## Common Issues and Fixes

- `psql` not found:
	- Reopen terminal or add PostgreSQL `bin` directory to PATH
- Password authentication failed:
	- Confirm username/password and host/port values
- Port 5432 already in use:
	- Change PostgreSQL port during install or in config
- Cannot connect to server:
	- Confirm PostgreSQL service is running in Windows Services
