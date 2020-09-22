.PHONY: dev build publish login clean clean-local aws-repo aws-network aws-fargate deploy deploy-test

aws-repo:
	aws cloudformation deploy --template-file ./aws/ecr.yml --stack-name fastapi-fargate-ecr

aws-network:
	aws cloudformation deploy --template-file ./aws/network.yml --capabilities CAPABILITY_IAM --stack-name fastapi-fargate-netowork

aws-fargate:
	aws cloudformation deploy --template-file ./aws/fargate.yml --stack-name fargate-svc-td

dev:
	docker build -t local-pause:latest ./containers/local-endpoint
	docker run -d -p 80:80 -p 5000:5000 --name local-pause --cap-add=NET_ADMIN local-pause 
	docker-compose -f docker-compose.yml -f docker-compose-local.yml up --build

build:
	docker-compose -f docker-compose.yml -f docker-compose-prod.yml build

publish:
	docker-compose push

login:
	$$(aws ecr get-login --no-include-email)

clean:
	docker-compose down -v

clean-local:
	docker-compose down -v
	docker stop local-pause
	docker rm local-pause
	
deploy/%:
	aws cloudformation deploy --template-file ./aws/fargate.yml --stack-name fargate-svc-td-$* 

deploy-test/%:
	aws cloudformation deploy --template-file ./aws/fargate.yml --stack-name fargate-svc-td-$*  \
	--parameter-overrides $$(cat ./aws/$*.json | jq -r '.Parameters|to_entries[]|.key+"="+.value')