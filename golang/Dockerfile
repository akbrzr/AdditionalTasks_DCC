FROM golang:1.20-alpine AS builder

WORKDIR /app
COPY . .
RUN go build -o app main.go

FROM gcr.io/distroless/static-debian12 AS runner

COPY --from=builder /app/app /app/app

ENTRYPOINT ["/app/app"]