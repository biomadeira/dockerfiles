REGISTRY = https://hub.docker.com/u
TAG=2.2
NAME = biomadeira/jabaws


.PHONY: all build push run test clean

all: build, push

build:
	docker pull $(NAME):$(TAG)
ifeq ($(LATEST), $(TAG))
	docker build --no-cache --rm -t $(NAME):$(TAG) -t $(IMAGE):latest .
else
	docker build --no-cache --rm -t $(NAME):$(TAG) .
endif

# docker login required for push
push:
	docker push $(NAME)

run:
	docker run --rm -it -p 8080:8080 biomadeira/jabaws:2.2

test:
	docker run --rm -it -p 8080:8080 biomadeira/jabaws:2.2

clean:
ifeq ($(strip $(NAME)),)
	echo "Nothing to delete"
else
	docker ps -a | awk '{ print $$1,$$2 }' | grep "$(NAME)" | awk '{print $$1 }' | xargs -I {} docker rm {}
endif
