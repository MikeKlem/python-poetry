ARG DISTRO=alpine
ARG PYTHONVERSION=3.13
ARG TAG=$PYTHONVERSION-$DISTRO
ARG IMAGE=python

FROM $IMAGE:$TAG

ARG POETRY_HOME=/opt/poetry

RUN python -m venv $POETRY_HOME && \
    $POETRY_HOME/bin/pip install --upgrade pip setuptools wheel
    # jsonschema 4.18 uses Rust-based libraries which causes issues when building from source
RUN $POETRY_HOME/bin/pip install "jsonschema<4.18.0" && \
    $POETRY_HOME/bin/pip install poetry 

COPY . $POETRY_HOME
WORKDIR $POETRY_HOME

RUN apk add gcc python3-dev musl-dev linux-headers
ENTRYPOINT [ "$POETRY_HOME/bin/poetry install && \
    $POETRY_HOME/bin/poetry run pytest --junitxml=junit.xml -v " ]
