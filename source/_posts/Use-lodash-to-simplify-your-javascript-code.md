---
title: Use lodash to simplify your javascript code
tags: |-

  - code
permalink: use-lodash-to-simplify-your-javascript-code
id: 6
updated: '2016-11-22 09:28:59'
date: 2016-11-22 00:16:27
---

Recall the following code? You need to retrieve a property value deep in an object. It smells, doesn't it? 
How can we write it better? 

```
const extractFirstErrorDetails = (errorResponse) => {
    if (errorResponse) {
        const data = errorResponse.data;
        if(data) {

            if(data.errors) {
                if(data.errors[0]) {
                    const errorDetails = data.errors[0].detail;
                    if(errorDetails) {
                        return errorDetails;
                    }
                }

            }
        }
    }
    return "";
};
```
**using lodash**

`_.get(errorResponse, 'data.errors[0].detail', '')`

this is the [lodash get method](https://lodash.com/docs/4.16.6#get)
> _.get(object, path, [defaultValue])

Gets the value at path of object. If the resolved value is undefined, the defaultValue is returned in its place.
