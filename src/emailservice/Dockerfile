FROM python:3.12.8-alpine AS builder


RUN apk update \
    && apk add --no-cache g++ linux-headers \
    && rm -rf /var/cache/apk/*

# get packages
COPY requirements.txt ./
RUN pip install -r requirements.txt

FROM python:3.12.8-alpine

# Enable unbuffered logging
ENV PYTHONUNBUFFERED=1
# Enable Profiler
ENV ENABLE_PROFILER=1

WORKDIR /email_server

# run pip install, the installed libraries will go to directory /usr/local/lib/python3.12/

COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/

COPY . .

EXPOSE 8080
ENTRYPOINT [ "python", "email_server.py" ]