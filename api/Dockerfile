# multistage docker build. This reduces the size of the final docker image.
# stage 1 to build the app =>  build stage
FROM golang:alpine as builder

RUN mkdir /build

ADD . /build/

WORKDIR /build

RUN go build -o main .

# stage 2 deploys the app built in stage 1 => Runtime stage

FROM alpine

RUN adduser -S -D -H /app appuser

USER appuser

COPY . /app

COPY --from=builder /build/main /app/

WORKDIR /app

EXPOSE 3000

CMD ["./main"]

# RUN: is used during the build process to execute commands and create a new image layer.
# CMD: is used to provide a default command for the container to run when started. 
# It can be overridden when starting a container.