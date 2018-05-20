---
title: How to use custom authorizer for aws api gateway
tags: |-

  - code
  - aws
permalink: aws-api-gateway-custom-authorizer
id: 7
updated: '2016-12-08 23:52:21'
date: 2016-11-24 09:46:18
---

The customer authoriser is a lambda you created. API gateway use it to authorize the client requests for the configured APIs. Which accepts token, verify it and return IAM policy.

For a valid policy, API Gateway caches the returned policy, associated with the incoming token and used for the current and subsequent requests, over a pre-configured time-to-live (TTL) period of **up to 3600 seconds**. You can set the TTL period to zero seconds to disable the policy caching. The default TTL value is **300** seconds. Currently, the maximum TTL value of 3600 seconds cannot be increased.

Serverless framework supports this feature by setting **resultTtlInSeconds** in authorizer.

``` events:
      - http:
          path: partners
          method: get
          integration: lambda
          authorizer:
            name: Authorizer
            identitySource: method.request.header.Authorization
            resultTtlInSeconds: 180
```

ref: 
https://aws.amazon.com/blogs/compute/introducing-custom-authorizers-in-amazon-api-gateway/
https://github.com/awslabs/aws-apigateway-lambda-authorizer-blueprints
http://docs.aws.amazon.com/apigateway/latest/developerguide/use-custom-authorizer.html
