FROM python:3.11-slim

WORKDIR /app

RUN pip install --no-cache-dir hatchling packaging

COPY pyproject.toml .
COPY agent/ agent/

RUN pip install --no-cache-dir .

RUN useradd -r -u 1000 appuser && chown -R appuser /app
USER appuser

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PORT=8000

EXPOSE 8000

CMD ["uvicorn", "agent.main:app", "--host", "0.0.0.0", "--port", "8000"]
