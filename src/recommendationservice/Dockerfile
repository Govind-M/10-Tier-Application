FROM python:3.12.8-alpine AS builder

WORKDIR /usr/src/app

RUN apk update \
    && apk add --no-cache g++ linux-headers \
    && rm -rf /var/cache/apk/*

COPY requirements.txt .
RUN pip install -r requirements.txt    

FROM python:3.10.8-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /recomendationservice

COPY --from=builder /usr/local/lib/python3.12/ ./usr/local/lib/python3.12/

COPY . .

ENV PORT "8080"
EXPOSE 8080

ENTRYPOINT ["python", "recommendation_server.py"]