# GRPC Guide

## Main Compiler
Download ```protoc``` binary from https://github.com/protocolbuffers/protobuf/releases and save in your bin folder, make sure its accessible and executable.

## Install plugin
### GO
```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.26
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.1
```
Don't forget to export Go Path bin folder
```bash
export PATH="$PATH:$(go env GOPATH)/bin"
```

### Javascript (WEB/Vue)
Download ```protoc-gen-grpc-web``` plugin from https://github.com/grpc/grpc-web/releases and save in your bin folder, make sure its accessible and executable.

### Typescript
Install  plugin via node package manager e.g yarn.
```bash
yarn global add protoc-gen-ts
```

## Compile Protobuf
Place ```*.proto``` file in the same directory as the ```Makefile```. Then run ```make```.
Makefile samples:
```Makefile
.PHONY = all

all:
	make prepare
	make compile

prepare:
	rm -r -f go web ts
	mkdir go web ts

compile:
	@echo "Compiling protos..."
	protoc -I . *.proto --go_out=:go --go_opt=paths=source_relative --go-grpc_out=:go --go-grpc_opt=paths=source_relative --go-grpc_opt=require_unimplemented_servers=false
	protoc -I . *.proto --js_out=import_style=commonjs,binary:web --grpc-web_out=import_style=commonjs,mode=grpcwebtext:web
	protoc -I . *.proto --ts_out=import_style=commonjs,binary:ts
  ```
  
