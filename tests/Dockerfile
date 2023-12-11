ARG DISTRO slim-buster
ARG PYTHONVERSION 311
ARG TAG latest
ARG IMAGE python$PYTHONVERSION-$DISTRO

FROM $IMAGE:$TAG

ARG POETRY_HOME=/opt/poetry
    # jsonschema 4.18 uses Rust-based libraries which causes issues when building from source
RUN $PYTHON -m venv $POETRY_HOME && \
    $POETRY_HOME/bin/pip install --upgrade pip setuptools wheel && \
    $POETRY_HOME/bin/pip install "jsonschema<4.18.0" && \
    echo "PATH=$POETRY_HOME/bin:$PATH"

RUN poetry install && \
    poetry run pytest --junitxml=junit.xml -v
  
