FROM node:20.18.1-alpine AS builder

WORKDIR /usr/src/app

RUN apk add --update --no-cache \
    python3 \
    make \
    g++

COPY package*.json ./

RUN npm install --only=production

FROM alpine:3.20.3

WORKDIR /usr/src/app

RUN apk add --no-cache nodejs

COPY --from=builder /usr/src/app/node_modules ./node_modules

COPY . .

EXPOSE 50051
ENTRYPOINT [ "node", "index.js" ]