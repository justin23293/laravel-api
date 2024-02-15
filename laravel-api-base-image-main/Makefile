.PHONY: help ps build build-prod start fresh fresh-prod stop restart destroy \
	cache cache-clear migrate migrate migrate-fresh tests tests-html

CONTAINER_PHP=api
CONTAINER_REDIS=redis
CONTAINER_DATABASE=database

help: ## Print help.
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)

auth: #authenticate with AWS
	aws ecr get-login-password --region ap-southeast-2 | docker login --username AWS --password-stdin 154395601581.dkr.ecr.ap-southeast-2.amazonaws.com

build-push:
	make build
	make push

build:
	docker build -t prod-laravel-api-baseimage .

push:
	docker tag prod-laravel-api-baseimage:latest 154395601581.dkr.ecr.ap-southeast-2.amazonaws.com/prod-laravel-api-baseimage:latest
	docker push 154395601581.dkr.ecr.ap-southeast-2.amazonaws.com/prod-laravel-api-baseimage:latest
