FROM dhi.io/python:3.12.13-debian13-dev AS builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    UV_NO_DEV=1

COPY --from=ghcr.io/astral-sh/uv:0.11.7 /uv /uvx /bin/

COPY . .
RUN uv sync

FROM dhi.io/python:3.12.13-debian13

WORKDIR /app

COPY --from=builder --chown=65532:65532 /app /app
COPY --from=ghcr.io/astral-sh/uv:0.10.0 /uv /uvx /bin/

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

EXPOSE 8000
CMD ["uv", "run", "gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--access-logfile", "-", "--error-logfile", "-", "--log-level", "info"]
