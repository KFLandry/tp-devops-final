FROM  golang:1.23-alpine as builder
WORKDIR /app

COPY ./backend/go.mod ./backend/go.sum ./
RUN go mod download

COPY ./backend/ ./
RUN go build -o server ./cmd/server/main.go

FROM scratch
WORKDIR /app

COPY --from=builder /app/server .
EXPOSE 8080

CMD ["./server"]