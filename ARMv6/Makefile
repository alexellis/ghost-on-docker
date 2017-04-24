NS = alexellis2
VERSION ?= armv6-0.11.8
REPO = ghost-on-docker

.PHONY: build push shell run start stop rm release

build:
	docker build -t $(NS)/$(REPO):$(VERSION) .
push:
	docker push $(NS)/$(REPO):$(VERSION)

default: build

