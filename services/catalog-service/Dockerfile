FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY go.mod .
COPY main.go .

RUN CGO_ENABLED=0 GOOS=linux go build -o catalog-service .

FROM alpine:3.20

WORKDIR /app

COPY --from=builder /app/catalog-service .

EXPOSE 8080

HEALTHCHECK --interval=5s --timeout=2s --retries=5 \
  CMD wget -qO- http://localhost:8080/health || exit 1

CMD ["./catalog-service"]
