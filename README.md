## Add virtual env, CLASSIC method

`python -m venv env`

`source env/bin/activate`

`pip install Flask`

`python -m pip freeze > requirements.txt`

#### Install from requirements.txt:
`pip install -r requirements.txt`


## Add virtual env, with POETRY

`pip install poetry`

> Create or init existings project:

`poetry new <project_name>`
    or
`poetry init`

> Create lock:

`poetry lock`

> To Activate ENV:
`source $(poetry env info --path)/bin/activate`

> To Deactivate ENV: `deactivate`

> Examples poetry commands:

`poetry add aiosqlite`

`poetry remove aiosqlite`

`poetry install`

`poetry update`

`poetry show`

`poetry run pytest`

`poetry export --without-hashes --format=requirements.txt > requirements.txt`

## -= Example Makefile for poetry =-

Since you we are using poetry, there is no need to manually activate the virtual environment, poetry run automatically runs commands in it

```Makefile:
.PHONY: setup \
        lint \
        mypy \
        help

setup: ## Project setup
    poetry install

lint: ## Run linter
    poetry run ruff format --config ./pyproject.toml .
    poetry run ruff check --fix --config ./pyproject.toml .

mypy: ## Run mypy
    poetry run mypy ./

test: ## Run tests check
    poetry run pytest $(filter-out $@,$(MAKECMDGOALS)) -s

# Just help
help: ## Display help screen
    @grep -h -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'```
