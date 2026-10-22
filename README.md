<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e3a8a,100:3b82f6&height=170&section=header&text=Finance%20Management%20App&fontColor=ffffff&fontSize=44&fontAlignY=38&desc=Django%20web%20app%20for%20tracking%20personal%20income%20and%20expenses&descAlignY=60&descSize=16" alt="Finance Management App" />

![Python](https://img.shields.io/badge/Python-3-3776ab?style=flat-square&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-3.x-092e20?style=flat-square&logo=django&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169e1?style=flat-square&logo=postgresql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952b3?style=flat-square&logo=bootstrap&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-ff6384?style=flat-square&logo=chartdotjs&logoColor=white)
![Heroku](https://img.shields.io/badge/Heroku-ready-430098?style=flat-square&logo=heroku&logoColor=white)

</div>

A server-rendered Django application where users register, record their **income and expenses**, search and edit entries, and see where their money goes in charts.

## ✨ Features

- 🔐 **Registration and login** with username/email validation endpoints and **email account activation** (users are inactive until they click the emailed link)
- 💸 **Expenses** and 💰 **income**: add, edit, delete, paginated lists and live search
- 🗂️ Expense categories and income sources, each entry owned by a user
- 📊 **Stats page** with Chart.js visualisations (expense totals per category)
- 💱 **Currency preference** per user, chosen from a bundled `currencies.json`
- 🛠️ Django admin with custom templates

## 🏗️ Architecture

Classic Django MVT split into one app per concern:

| App | Responsibility |
| --- | --- |
| `authentication` | Register, login/logout, validation endpoints, email activation |
| `expenses` | `Expense` and `Category` models, CRUD, search, category summary, stats |
| `userincome` | `UserIncome` and `Source` models, CRUD, search |
| `userpreferences` | One-to-one `UserPreference` (currency) per user |
| `expenseswebsite` | Project settings, URLs, static assets (JS charts, CSS) |

## 🧰 Tech stack

| Layer | Technology |
| --- | --- |
| Backend | Django, `validate-email`, `six` |
| Database | PostgreSQL via `psycopg2`, configured with environment variables |
| Frontend | Django templates, Bootstrap, vanilla JS, Chart.js |
| Deployment | `gunicorn`, `django-heroku`, `Procfile` |

## 🚀 Getting started

```bash
git clone https://github.com/Brian-Dol/Finance-management-application-Django.git
cd Finance-management-application-Django
pipenv install            # Pipfile targets Python 3.7
```

Set the variables listed in `.env-example`, plus the SMTP settings used for activation emails:

```bash
export DB_NAME=... DB_USER=... DB_USER_PASSWORD=... DB_HOST=...
export EMAIL_HOST=... EMAIL_HOST_USER=... EMAIL_HOST_PASSWORD=...
```

```bash
pipenv run python manage.py migrate
pipenv run python manage.py runserver
```

Open http://127.0.0.1:8000/ and register an account.

## 📁 Project structure

```
authentication/   expenses/   userincome/   userpreferences/
expenseswebsite/  # settings, urls, static (css, js)
templates/        # base, auth, expenses, income, preferences
currencies.json  Procfile  Pipfile
```

## 🗺️ Notes

- `SECRET_KEY` is hard-coded and `DEBUG = True` in `settings.py`; move both to environment variables before any real deployment.
- Amounts are stored as `FloatField` (a `DECIMAL` would be safer for money).
- The dependency pins (Python 3.7, `psycopg2==2.7.7`) are old and may need updating on modern systems.
- Automated tests are not yet written.

## 👤 Author

**Brian Dol**, Senior Full Stack Engineer · [Portfolio](https://portfolio.dol-brian23.workers.dev/) · [LinkedIn](https://linkedin.com/in/brian-dol-31a06115a/)
