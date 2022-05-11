# syntax=docker/dockerfile:1.4
FROM golang:1.18-alpine

RUN apk add --no-cache openssh-client git
RUN mkdir -p -m 0700 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts
RUN --mount=type=ssh git clone git@github.com:ndeloof/toolbox.git

RUN --mount=type=secret,id=mysecret cat /run/secrets/mysecret

WORKDIR /app
EXPOSE 5050
COPY go.* ./

RUN go mod download
COPY *.go ./
RUN go build -o /demo

CMD [ "/demo" ]