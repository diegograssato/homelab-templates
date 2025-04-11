default: build

DOCKER_IMAGE ?= diegograssato/devops-tools
GIT_BRANCH ?= $(shell git rev-parse --abbrev-ref HEAD)
.PHONY: test \
	build \
	push
 

ifeq ($(GIT_BRANCH), main)
	DOCKER_TAG = latest
else
	DOCKER_TAG = $(GIT_BRANCH)
endif

build:
	@docker build \
	  --build-arg VCS_REF=`git rev-parse --short HEAD` \
	  --build-arg BUILD_DATE=`date -u +"%Y-%m-%dT%H:%M:%SZ"` \
	  -t $(DOCKER_IMAGE):latest .
	  
push: build
	# Push to DockerHub
	docker push $(DOCKER_IMAGE):latest

test: build
	docker run $(DOCKER_IMAGE):$(DOCKER_TAG) version --client
