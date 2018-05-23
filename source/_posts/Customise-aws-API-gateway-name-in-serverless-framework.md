---
title: Customise aws API gateway name in serverless framework
tags: [code, aws]
permalink: customize-aws-api-gateway-name-in-serverless-framework
id: 14
updated: '2017-03-08 11:32:06'
date: 2017-02-22 01:00:16
---

### serverless framework

When using serverless framework to deploy aws api gateway, by default the api name will be stage-servicename, like `sit-test-service` or `dev-test-service`.

If you want to customise the api name, you can do it through resources configuration.

```
serverless.yml

resources:
  Resources:
	ApiGatewayRestApi:
	  Type: AWS::ApiGateway::RestApi
	  Properties:
	    Name: "yourServiceName"
```

I use a seperate resource file, it looks like this

```
serverless.yml

resources:
   Resources: ${file(resources.yml)}	
```

```
resources.yml

ApiGatewayRestApi:
  Type: AWS::ApiGateway::RestApi
  Properties:
    Name: "yourServiceName"
```

- When you deploy again after adding custom api name, serverless will call `aws cloudformation update-stack` based on the cloudformation json template. It won't create a new api, just rename it by updating the existing api. The existing api id won't change, so the existing cloudfront or custom dns won't be affected.

### CLI
if you want to do this via command line,

- first list APIS and IDs under your account:

```
aws apigateway get-rest-apis
```

- Use the Id to update name of API

```
aws apigateway update-rest-api --rest-api-id IDOfTheAPIThatNeedsTobeUpdated --patch-operations op=replace,path=/name,value=NewName
```


	    
	  
	  
    
    

