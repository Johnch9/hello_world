FROM golang:alpine as builder

ENV GO111MODULE=on

RUN apk update && apk add --no-cache git bash ca-certificates

RUN mkdir -p /app

WORKDIR /app


COPY . .

RUN go mod init /app/hello

RUN while true; do echo Keep alive... && sleep 600; done & \
        CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /app/hello /app/

