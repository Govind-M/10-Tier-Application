FROM golang:1.23.4-alpine AS builder

WORKDIR /usr/src/app


COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN go build -o /go/bin/productcatalogservice .

FROM alpine

WORKDIR /usr/src/app

COPY --from=builder /go/bin/productcatalogservice ./productcatalogservice
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt

COPY products.json ./

ENV GOTRACEBACK=single

EXPOSE 3550
ENTRYPOINT [ "./productcatalogservice" ]
