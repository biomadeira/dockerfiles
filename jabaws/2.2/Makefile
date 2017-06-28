REGISTRY = https://hub.docker.com/u
TAG=2.2
NAME = bartongroup/jabaws
IMAGE = $(REGISTRY)/$(NAME)


.PHONY: all build push run test clean

all: build

build:
	docker pull bartongroup/jabaws:2.2
ifeq ($(LATEST), $(TAG))
	docker build --no-cache --rm -t $(IMAGE):$(TAG) -t $(IMAGE):latest .
else
	docker build --no-cache --rm -t $(IMAGE):$(TAG) .
endif

# docker login required for push
push:
	docker push $(IMAGE)

run:
	docker run --rm -it -p 8080:8080 bartongroup/jabaws:2.2

test:
	docker run --rm -it -p 8080:8080 bartongroup/jabaws:2.2

clean:
ifeq ($(strip $(IMAGE)),)
	echo "Nothing to delete"
else
	docker ps -a | awk '{ print $$1,$$2 }' | grep "$(IMAGE)" | awk '{print $$1 }' | xargs -I {} docker rm {}
endif
