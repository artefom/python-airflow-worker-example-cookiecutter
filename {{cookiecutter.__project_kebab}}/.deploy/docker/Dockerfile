FROM python:3.11-slim-bullseye

WORKDIR /app

RUN pip install --no-input "poetry>=1.2.2<2.0"

# Install packages in a cache-friendly way
COPY poetry.lock ./
COPY pyproject.toml ./

# Configure credentials for distribusion pacakge repo
ARG GITLAB_REGISTRY_USERNAME
ARG GITLAB_REGISTRY_PASSWORD
RUN poetry config http-basic.distribusion $GITLAB_REGISTRY_USERNAME $GITLAB_REGISTRY_PASSWORD


RUN POETRY_VIRTUALENVS_CREATE=false poetry install --no-root

# Copy package source code
COPY ./{{cookiecutter.__project_slug}} ./{{cookiecutter.__project_slug}}

# Install package
RUN pip install --no-deps .

# Start single uvicorn worker
CMD {{cookiecutter.__project_kebab}}
