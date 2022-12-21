## Build and running
docker build -t phpmyfunction .
docker run -p 9000:8080 phpmyfunction:latest

### Post sample request 
https://xxxxx.execute-api.ap-northeast-1.amazonaws.com/dev/welcome

## Push to ECR
AWS_ACCOUNT_ID=xxxxx
AWS_DEFAULT_REGION=ap-northeast-1

aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com

docker tag phpmyfunction:latest $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/php:latest
docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/php:latest

## Performance
### Cold start
```
754ms
774ms
792ms
713ms
770ms
```

### Hot start
```
60ms
57ms
66ms
56ms
58ms
```
