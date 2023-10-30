# syntax=docker/dockerfile:1

# Comments are provided throughout this file to help you get started.
# If you need more help, visit the Dockerfile reference guide at
# https://docs.docker.com/engine/reference/builder/

# ARG PYTHON_VERSION=3.11.6
# FROM python:${PYTHON_VERSION}-slim as base

# ARG REGISTRY=quay.io
# ARG OWNER=jupyter
# ARG BASE_CONTAINER=$REGISTRY/$OWNER/base-notebook
# FROM $BASE_CONTAINER

FROM quay.io/jupyter/base-notebook


# Prevents Python from writing pyc files.
ENV PYTHONDONTWRITEBYTECODE=1

# Keeps Python from buffering stdout and stderr to avoid situations where
# the application crashes without emitting any logs due to buffering.
ENV PYTHONUNBUFFERED=1

USER root

# Download dependencies as a separate step to take advantage of Docker's caching.
# Leverage a cache mount to /root/.cache/pip to speed up subsequent builds.
# Leverage a bind mount to requirements.txt to avoid having to copy them into
# into this layer.
RUN --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    python -m pip install -r requirements.txt

COPY overrides.json /opt/conda/share/jupyter/lab/settings/overrides.json

WORKDIR '/Python Notebook'
RUN fix-permissions "/Python Notebook"

USER ${NB_UID}

EXPOSE 8888

CMD ["start.sh", "jupyter", "lab", "--NotebookApp.token=''"]
# CMD ["start-notebook.sh --notebookapp.token=''"]

