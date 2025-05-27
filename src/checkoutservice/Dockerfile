FROM golang:1.22-alpine as builder

WORKDIR /usr/src/app


COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN go build -o /go/bin/checkoutservice ./


FROM alpine

WORKDIR /usr/src/app

COPY --from=builder /go/bin/checkoutservice ./

ENV GOTRACEBACK=single

EXPOSE 5050
ENTRYPOINT [ "./checkoutservice" ]