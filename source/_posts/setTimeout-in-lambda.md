---
title: setTimeout in aws lambda
date: 2018-11-05 16:03:18
tags: [code, nodejs, aws, lambda]
---

```js
const slowMethod = () => {
  setTimeout(() => {
    console.log("setTimeout callback was called after 5 seconds.");
  }, 5000);
};

const handler = async () => {
  console.log("start");

  slowMethod();

  console.log("end");

  return {
    statusCode: 200,
    body: "lambda end"
  };
};

```
### setTimeout

1. local run with setTimeout
>start
>end
>Promise delay was called after 5 seconds.

slowMethod will print out after 5 seconds.

2. run on aws lambda with setTimeout
First time run, Lambda just ended the handler function without printing "setTimeout callback was called after 5 seconds.".
Second run, It prints "setTimeout callback was called after 5 seconds.” first and then the other ones!

05:05:00
START RequestId: 58a3472a-e0b8-11e8-8559-17192896f1c6 Version: $LATEST

05:05:00
2018-11-05T05:05:00.482Z	58a3472a-e0b8-11e8-8559-17192896f1c6	start

05:05:00
2018-11-05T05:05:00.484Z	58a3472a-e0b8-11e8-8559-17192896f1c6	end

05:05:00
END RequestId: 58a3472a-e0b8-11e8-8559-17192896f1c6

05:05:00
REPORT RequestId: 58a3472a-e0b8-11e8-8559-17192896f1c6	Duration: 5.72 ms	Billed Duration: 100 ms Memory Size: 1024 MB	Max Memory Used: 49 MB

05:06:17
START RequestId: 86f9763f-e0b8-11e8-9200-4b9da457c7b4 Version: $LATEST

05:06:17
2018-11-05T05:06:17.818Z	58a3472a-e0b8-11e8-8559-17192896f1c6	setTimeout callback was called after 5 seconds.

05:06:17
2018-11-05T05:06:17.832Z	86f9763f-e0b8-11e8-9200-4b9da457c7b4	start

05:06:17
2018-11-05T05:06:17.832Z	86f9763f-e0b8-11e8-9200-4b9da457c7b4	end

05:06:17
END RequestId: 86f9763f-e0b8-11e8-9200-4b9da457c7b4

05:06:17
REPORT RequestId: 86f9763f-e0b8-11e8-9200-4b9da457c7b4	Duration: 13.69 ms	Billed Duration: 100 ms Memory Size: 1024 MB	Max Memory Used: 49 MB

3. add await before slowMethod which uses setTimeout
no difference

### Promise.delay

4. change setTimeout to Promise.delay(5000)
same as setTimeout

4. add await before slowMethod
out put is below, same on local and aws lambda. The duration is 5008ms

>start
>Promise delay was called after 5 seconds.
>end

### Slow http request

1. call a slow api with await
  Same as 4 above, await the api to complete.
  The lmabda will wait and billed duration time is the real time(5.2s).

2. call a slow api without await
   The lambda doesn't wait(100ms) and the api was not called.
   no magic happen on the second call, not like case 2 above. Looks like the http request was killed.

2.1 remove async before handler will be similar like case 1, call api after log 'end', duration is > 5 seconds.

2.2 remove handler async make case 1 also changed the lambda to wait for slowMethod to finish in 5s.


### Why?

Background processes or callbacks initiated by your Lambda function that did not complete when the function ended, will resume if AWS Lambda chooses to reuse the Execution Context.

This statement is true for setTimeout, but not for http request.


https://medium.com/radient-tech-blog/aws-lambda-and-the-node-js-event-loop-864e48fba49
https://forum.serverless.com/t/aws-lambda-unable-to-make-external-api-call/4556/4
