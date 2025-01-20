FROM python:3.10-slim


ENV APP_ENV=production \
    APP_DEBUG=false

RUN groupadd -r usergroup && useradd -r -g usergroup user

WORKDIR /app
RUN chown user:usergroup /app

COPY --chown=user:usergroup requirements.txt .


RUN apt-get update && \
    apt-get install -y build-essential && \
    pip install --no-cache-dir -r requirements.txt && \
    apt-get purge -y build-essential && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

COPY --chown=user:usergroup . .

USER user

EXPOSE 8080

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8080", "app:app"]
