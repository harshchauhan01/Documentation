# Django Guide

## What is Django?

Django is a high-level Python web framework used to build secure, scalable web applications quickly. It includes many built-in features so you do not have to build everything from scratch.

Key points:
- Written in Python
- Follows the MVT pattern (Model, View, Template)
- Includes admin panel, ORM, authentication, routing, forms, and security features
- Great for backend APIs and full-stack web apps

## Prerequisites

Before creating a Django project, make sure you have:
- Python 3.10+ installed
- `pip` available
- VS Code or another editor
- Terminal access (PowerShell on Windows)

Check versions:

```powershell
python --version
pip --version
```

## Create a Django Project (Step by Step)

### 1. Create and open a project folder

```powershell
mkdir django_project
cd django_project
```

### 2. Create a virtual environment

```powershell
python -m venv .venv
```

### 3. Activate the virtual environment

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks scripts, run this once:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate again.

### 4. Install Django

```powershell
pip install django
```

### 5. Create a Django project

```powershell
django-admin startproject <project_name> .
```

This creates the project in your current folder.

### 6. Run initial migrations

```powershell
python manage.py migrate
```

### 7. Start the development server

```powershell
python manage.py runserver
```

Open in browser:
- http://127.0.0.1:8000/

## Create Your First Django App

Inside the same project folder:

```powershell
python manage.py startapp <app_name>
```

Add the app to `INSTALLED_APPS` in `config/settings.py`:

```python
INSTALLED_APPS = [
		# default apps...
		'<app_name>',
]
```

## Minimal Hello Page Setup

### 1. Add a view in `core/views.py`

```python
from django.http import HttpResponse

def home(request):
		return HttpResponse("Hello from Django!")
```

### 2. Create `core/urls.py`

```python
from django.urls import path
from .views import home

urlpatterns = [
		path('', home, name='home'),
]
```

### 3. Include app URLs in `config/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
		path('admin/', admin.site.urls),
		path('', include('core.urls')),
]
```

Restart server and visit:
- http://127.0.0.1:8000/

## Useful Django Commands

```powershell
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## Typical Project Structure

```text
django_project/
	.venv/
	config/
		settings.py
		urls.py
		wsgi.py
	core/
		views.py
		models.py
		urls.py
	manage.py
```

## Freeze Dependencies

```powershell
pip freeze > requirements.txt
```

Install later with:

```powershell
pip install -r requirements.txt
```

## Common Issues and Fixes

- `python` not found:
	- Reinstall Python and enable "Add Python to PATH"
- Virtual environment not activating:
	- Check path: `.\.venv\Scripts\Activate.ps1`
- Port already in use:
	- Run server on another port: `python manage.py runserver 8001`

