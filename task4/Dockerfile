FROM python:3.10-slim as builder

WORKDIR /build

COPY requirements.txt .

RUN python -m venv /venv && \
    . /venv/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

FROM python:3.10-slim

WORKDIR /app

COPY --from=builder /venv /venv

COPY app.py .

ENV PATH="/venv/bin/:$PATH"

EXPOSE 5000

CMD ["python", "app.py"]
