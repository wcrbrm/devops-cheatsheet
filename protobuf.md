# Protobuf

## INSTALLING
```
PROTOC_VERSION=3.9.1
PROTOC_ZIP=protoc-${PROTOC_VERSION}-linux-x86_64.zip
PROTOC_INCLUDES= \
    -I$$GOPATH/src/github.com/grpc-ecosystem/grpc-gateway/third_party/googleapis \
	-I$$GOPATH/src/github.com/grpc-ecosystem/grpc-gateway/ 
PROTOC_PLUGINS=grpc

curl -OL https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/${PROTOC_ZIP}
sudo unzip -o ${PROTOC_ZIP} -d /usr/local bin/protoc
sudo unzip -o ${PROTOC_ZIP} -d /usr/local include/*
rm -f ${PROTOC_ZIP}
go get -u github.com/golang/protobuf/protoc-gen-go
go get -u github.com/amsokol/protoc-gen-gotag
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger
go get -u google.golang.org/grpc

```

## VS CODE

```
https://github.com/zxh0/vscode-proto3
```

`.vscode/settings.json` example:
```
{
    "protoc": {
        "path": "/usr/local/bin/protoc",
        "options": [
            "--proto_path=${env.GOPATH}/src",
            "--proto_path=${env.GOPATH}/src/github.com/grpc-ecosystem/grpc-gateway/third_party/googleapis", 
            "--proto_path=${env.GOPATH}/src/github.com/grpc-ecosystem/grpc-gateway/", 
            "--proto_path=${env.GOPATH}/src/github.com/amsokol/"
        ]
    }
}
```


## RUNNING

```
protoc -I . $(PROTOC_INCLUDES) \
	-go_out=plugins=$(PROTOC_PLUGINS):. \
	--grpc-gateway_out=logtostderr=true:. \
	--swagger_out=json_names_for_fields=true:. \
	./*.proto
```

## MONGO

```
go get -u github.com/amsokol/mongo-go-driver-protobuf
go get -u github.com/amsokol/protoc-gen-gotag

```

```
https://github.com/amsokol/mongo-go-driver-protobuf
https://medium.com/@amsokol.com/new-official-mongodb-go-driver-and-google-protobuf-making-them-work-together-6357b0118f3f
```

## JSON Marshalling
```
https://iximiuz.com/en/posts/truly-optional-scalar-types-in-protobuf3/
```
Вне grpc-шлюза, если вы хотите упорядочить ваше сообщение буфера протокола, 
используйте пакет `github.com/golang/protobuf/jsonpb` вместо `encoding/json`


Избавление от `omitempty`:
```
ls *.pb.go | xargs -n1 -IX bash -c 'sed s/,omitempty// X > X.tmp && mv X{.tmp,}'
```



## Protobuf from OpenAPI

```
go get -u github.com/NYTimes/openapi2proto/cmd/openapi2proto
```

