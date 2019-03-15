FROM golang:latest AS build

ADD . /app/backend
WORKDIR /app/backend
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -o /backend .
ENV ALLOWED_ORIGIN='http://localhost:3000' 
ENV REDIS_ADDR=localhost:6379 


# Deploy in PRD stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=build /backend ./
RUN chmod +x ./backend
ENTRYPOINT ["./backend"]
EXPOSE 8080