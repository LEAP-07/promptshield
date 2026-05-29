FROM python:3.11-slim

WORKDIR /app

RUN pip install --no-cache-dir hatchling packaging

# Install the promptshield SDK first
COPY sdk/ /sdk/
RUN pip install --no-cache-dir /sdk/

# Install victim-agent
COPY victim-agent/pyproject.toml .
COPY victim-agent/agent/ agent/
RUN pip install --no-cache-dir .

RUN useradd -r -u 1000 appuser && chown -R appuser /app
USER appuser

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PORT=8000

EXPOSE 8000

CMD ["uvicorn", "agent.main:app", "--host", "0.0.0.0", "--port", "8000"]
