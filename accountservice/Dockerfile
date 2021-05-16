FROM golang:1.16-alpine3.13 AS builder

# ENV CGO_ENABLED 0

ADD . /go/src/accountservice

WORKDIR  /go/src/accountservice

# RUN mv ./healthchecker-linux-amd64 ../

RUN go get ./
RUN go build -o accountservice-linux-amd64 .

HEALTHCHECK --interval=3s --timeout=3s CMD ["./healthchecker-linux-amd64", "-port=6767"] || exit 1

# CMD if [ ${APP_ENV} = production ]; \
# 	then \
# 	app; \
# 	else \
# 	go get github.com/pilu/fresh && \
# 	fresh; \
# 	fi

 EXPOSE 6767

 ENTRYPOINT ["./accountservice-linux-amd64", "-configServerUrl=http://configserver:8888", "-profile=test", "-configBranch=P8"]