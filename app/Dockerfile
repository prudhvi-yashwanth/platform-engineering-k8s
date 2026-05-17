# Build stage
FROM golang:1.26.3-alpine AS builder

WORKDIR /app

COPY go.mod ./

RUN go mod download

COPY . .

RUN go build -o go-api ./cmd/api/main.go

# Runtime stage
FROM alpine:3.22

WORKDIR /app

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copy binary
COPY --from=builder /app/go-api .

# Set ownership
RUN chown -R appuser:appgroup /app

EXPOSE 8080

# Run as non-root numeric user
USER 1001

CMD ["./go-api"]