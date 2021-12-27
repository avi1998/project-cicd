# TODO

# We use Golang version 1.15.14 for the build, with the 
# environment variable CGO_ENABLED set to 0.

# Run the build scripts:
#  - src/stock-api/restore.sh
#  - src/stock-api/build.sh
#  you'll need to make the files executable first with chmod +x <filename>.

# Build output is a single executable file:
#  /server

# The app should run on a minimal OS.

# We need to set four environment variables - 
# GOLANG_VERSION and APP_VERSION - expected by ops
# CACHE_EXPIRY_SECONDS set to 45
# POSTGRES_CONNECTION_STRING set to "host=products-db port=5432 user=postgres password=widgetario dbname=postgres sslmode=disable"

# The startup command needs to run the executable from the build:
#  /server

# We also need to create an empty directory at /cache.
FROM golang:1.15.14-alpine3.14 AS builder
ENV CGO_ENABLED=0

WORKDIR /go/stock-api
COPY src/stock-api/. .

RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh  && ./build.sh

# app
FROM alpine:3.14

ENV POSTGRES_CONNECTION_STRING="host=products-db port=5432 user=postgres password=widgetario dbname=postgres sslmode=disable" \
    CACHE_EXPIRY_SECONDS="45" \
    GOLANG_VERSION="1.15.14" \
    APP_VERSION="0.4.0"

EXPOSE 8080
CMD ["/app/server"]

WORKDIR /cache
WORKDIR /app
COPY --from=builder /server .