# django-practise

Django practice project. The Django project lives in `blog/` (contains `manage.py`, the `blog` settings package and the `posts` app).

```
django-practise/
├── django_env/          # virtual environment (do not commit)
├── blog/
│   ├── manage.py        # run all Django commands from this folder
│   ├── requirement.txt
│   ├── db.sqlite3
│   ├── blog/            # project package (settings.py, urls.py, ...)
│   └── posts/           # app
└── README.md
```

> **Important:** run `python manage.py ...` from `blog/` (where `manage.py` is), not from the repo root or `blog/blog/`.

---

## 1. First-time setup

### Create and activate a virtual environment

```powershell
# from the repo root (PowerShell)
python -m venv django_env          # or: uv venv django_env
.\django_env\Scripts\Activate.ps1
```

```bash
# Git Bash
source django_env/Scripts/activate
```

```bash
deactivate                          # leave the venv
```

### Install dependencies

```bash
pip install -r blog/requirement.txt   # or: uv pip install -r blog/requirement.txt
pip install django                    # if starting fresh
pip freeze > blog/requirement.txt     # save installed packages
```

### Troubleshooting

| Error | Cause / fix |
|-------|-------------|
| `Couldn't import Django...` | Django is not installed in the active Python. Activate `django_env` and run `pip install django`, or `deactivate` to use the global Python. |
| `can't open file '...manage.py'` | Wrong folder. `cd blog` (and make sure you are not in `blog/blog`). |

---

## 2. Django commands

Run all of these from `blog/` with the venv active.

### Project and app

```bash
django-admin startproject <name>        # new project
django-admin startproject <name> .      # new project in current folder
python manage.py startapp <app>         # new app (e.g. posts); add it to INSTALLED_APPS in settings.py
```

### Database

```bash
python manage.py makemigrations         # create migrations from model changes
python manage.py makemigrations <app>   # for one app
python manage.py migrate                # apply migrations
python manage.py showmigrations         # list migrations and status
python manage.py sqlmigrate <app> 0001  # show SQL for a migration
python manage.py migrate <app> zero     # roll an app back fully
python manage.py dbshell                # open the DB shell
```

### Run and inspect

```bash
python manage.py runserver              # http://127.0.0.1:8000/
python manage.py runserver 8080         # custom port
python manage.py shell                  # interactive shell with Django loaded
python manage.py check                  # check the project for problems
python manage.py test                   # run tests
python manage.py collectstatic          # gather static files (deployment)
```

### Users and admin

```bash
python manage.py createsuperuser        # create admin user (admin at /admin/)
python manage.py changepassword <user>
```

### Typical workflow after editing models

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

---

## 3. Git and GitHub commands

Remote: `https://github.com/jayshankarprasad/django-practise.git`

### Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init                                # start a repo (already done here)
git clone <url>                         # copy a remote repo
git remote add origin <url>             # link a remote
git remote -v                           # show remotes
```

### Daily workflow

```bash
git status                              # what changed
git add <file>                          # stage a file
git add .                               # stage everything
git commit -m "message"                 # commit
git push origin main                    # push to GitHub
git pull origin main                    # fetch + merge from GitHub
git fetch                               # fetch without merging
```

### Inspect

```bash
git log --oneline                       # short history
git diff                                # unstaged changes
git diff --staged                       # staged changes
git show <commit>                       # one commit's changes
```

### Branches

```bash
git branch                              # list branches
git branch <name>                       # create
git checkout <name>                     # switch (or: git switch <name>)
git checkout -b <name>                  # create and switch
git merge <name>                        # merge into current branch
git branch -d <name>                    # delete merged branch
git push -u origin <name>               # push a new branch
```

### Undo

```bash
git restore <file>                      # discard unstaged changes to a file
git restore --staged <file>             # unstage
git commit --amend                      # edit the last commit message
git revert <commit>                     # new commit that undoes a commit
git stash / git stash pop               # shelve and restore changes
```

### Pull requests (GitHub CLI)

```bash
gh auth login
gh pr create --fill
gh pr list
gh pr merge
```

### Suggested `.gitignore`

```
django_env/
__pycache__/
*.pyc
db.sqlite3
.env
```

---

## 4. Quick start (copy/paste)

```powershell
git clone https://github.com/jayshankarprasad/django-practise.git
cd django-practise
python -m venv django_env
.\django_env\Scripts\Activate.ps1
pip install -r blog\requirement.txt
cd blog
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```
