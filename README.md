# Django Basic Tutorial – Polls App

This project is a beginner-friendly Django application based on the classic **polls** tutorial structure.
It demonstrates how to:

- define database models (`Question`, `Choice`)
- create views and URL routing
- render HTML templates with dynamic data
- use Django Admin to manage content

The app currently lets you list recent questions and open a detail page for each question.

---

## What this project does

### Main features

- `Question` model with publication date
- `Choice` model linked to each question
- Poll index page: shows latest 5 questions
- Poll detail page: shows a question and its choices
- Placeholder endpoints for results and voting
- Admin integration for creating/editing questions and choices
- SQLite database (`db.sqlite3`) for local development

### URL map

- `/polls/` → list recent questions
- `/polls/<question_id>/` → question detail
- `/polls/<question_id>/results/` → placeholder results response
- `/polls/<question_id>/vote/` → placeholder vote response
- `/admin/` → Django admin panel

---

## Project structure (important files)

- `manage.py` – Django management entry point
- `misite/settings.py` – project settings (installed apps, DB, templates)
- `misite/urls.py` – root URL configuration
- `polls/models.py` – `Question` and `Choice` models
- `polls/views.py` – app views (index/detail/results/vote)
- `polls/urls.py` – app URL routes
- `polls/templates/polls/` – HTML templates

---

## Prerequisites

- Python 3.10+
- `pip`

> This project was generated with Django 6.x style defaults.

---

## Setup and run

Run these commands from the project root (where `manage.py` is):

```bash
# 1) Create and activate virtual environment
python3 -m venv .venv
source .venv/bin/activate

# 2) Install Django
pip install "Django>=6,<7"

# 3) Apply migrations
python manage.py migrate

# 4) (Optional) Create admin user
python manage.py createsuperuser

# 5) Start development server
python manage.py runserver
```

Open in browser:

- http://127.0.0.1:8000/polls/
- http://127.0.0.1:8000/admin/

---

## Add sample poll data

If `/polls/` shows “No polls are available.”, add data via admin or shell.

### Option A: Django Admin

1. Go to `/admin/`
2. Log in with your superuser
3. Create `Question` and related `Choice` records

### Option B: Django shell

```bash
python manage.py shell
```

```python
from django.utils import timezone
from polls.models import Question, Choice

q = Question.objects.create(question_text="What is your favorite language?", pub_date=timezone.now())
Choice.objects.create(question=q, choice_text="Python", votes=0)
Choice.objects.create(question=q, choice_text="JavaScript", votes=0)
```

Then refresh `/polls/`.

---

## Useful commands

```bash
# Make migrations after model changes
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Run development server on a custom port
python manage.py runserver 8080

# Run tests
python manage.py test
```

---

## Current limitations

- `results` and `vote` views are placeholders (text responses only)
- No custom tests implemented yet in `polls/tests.py`
- Default development settings are enabled (`DEBUG=True`)

---

## Learning goals covered

This repository is a good reference for learning:

- Django app/project structure
- models and relationships (`ForeignKey`)
- URL routing with path parameters
- template rendering with context
- basic admin setup

If you want, the next practical step is implementing real vote submission and result counting in `polls/views.py`.
