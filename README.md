## Build and running
docker build -t phpmyfunction .
docker run -p 9000:8080 phpmyfunction:latest

### Post sample request 
curl "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{"queryStringParameters": {"name":"Ben"}}' -s | jq

## Push to ECR
AWS_ACCOUNT_ID=114264163394
AWS_DEFAULT_REGION=ap-northeast-1

av exec tgoto63 -- aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com

docker tag phpmyfunction:latest $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/php:latest
docker push 114264163394.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/php:latest