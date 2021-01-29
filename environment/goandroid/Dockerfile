FROM golang:1.14

ARG APP_NAME
ARG PORT 
ARG TARGET

COPY ./app/src /go/src/${APP_NAME}
WORKDIR /go/src/${APP_NAME}

RUN go get ./

RUN go get golang.org/x/mobile/cmd/gomobile

RUN gomobile init


RUN go mod init bug512/GoAndroid

RUN go get -d golang.org/x/mobile/example/basic

RUN go mod download

RUN go get github.com/githubnemo/CompileDaemon

#ENTRYPOINT CompileDaemon --build="gomobile build -target=${TARGET} -o build/${APP_NAME}" --command=./${APP_NAME}
ENTRYPOINT CompileDaemon --build="gomobile build -target=${TARGET} -o build/${APP_NAME} golang.org/x/mobile/example/basic" --command=./${APP_NAME}
#RUN go build -o ${APP_NAME}

#CMD go run main.go

#CMD ./${APP_NAME}

EXPOSE ${PORT}