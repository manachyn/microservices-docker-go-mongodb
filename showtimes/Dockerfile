FROM golang:1.19.3-alpine AS builder
WORKDIR /opt/app/
COPY showtimes/go.mod showtimes/go.sum ./
RUN go mod download
COPY showtimes/cmd ./cmd
COPY showtimes/pkg ./pkg
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o showtimes ./cmd/app

FROM alpine:3.17.3
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /opt/app/showtimes .
EXPOSE 4000
CMD ["./showtimes"]