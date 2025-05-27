FROM golang:1.23.4-alpine AS builder

WORKDIR /usr/src/app

RUN apk add --no-cache ca-certificates git
RUN apk add build-base

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o /go/bin/frontend ./

FROM alpine:3.18.2

WORKDIR /usr/src/app

RUN apk add --no-cache ca-certificates \
    busybox-extras net-tools bind-tools

COPY --from=builder /go/bin/frontend ./
COPY ./templates ./templates
COPY ./static ./static

ENV GOTRACEBACK=single

EXPOSE 8080
ENTRYPOINT [ "./frontend" ]