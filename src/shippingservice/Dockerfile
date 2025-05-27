FROM golang:1.23.4-alpine as builder

WORKDIR /usr/src/app


COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o /go/bin/shippingservice .

FROM alpine

RUN apk add --no-cache ca-certificates

WORKDIR /usr/src/app

COPY --from=builder /go/bin/shippingservice ./shippingservice

ENV APP_PORT=50051
ENV GOTRACEBACK=single


EXPOSE 50051
ENTRYPOINT [ "./shippingservice" ]
