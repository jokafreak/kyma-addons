RELEASE?=0.0.7
APP?=github-event-gw
GOOS?=linux
GOARCH?=amd64
DOCKER_ACCOUNT?=gabbi
CONTAINER_IMAGE?=${DOCKER_ACCOUNT}/${APP}

clean:
	rm -rf ${APP}

vet:
	GO111MODULE=on go vet .

test:
	GO111MODULE=on go test -v -race ./...

build: clean vet test
	GO111MODULE=on CGO_ENABLED=0 GOOS=${GOOS} GOARCH=${GOARCH} go build \
		-ldflags "-s -w" \
		-o ${APP}

build-image: build
	docker build -t $(CONTAINER_IMAGE):$(RELEASE) .

push-image: build-image
	docker push $(CONTAINER_IMAGE):$(RELEASE)

tidy:
	GO111MODULE=on go mod tidy