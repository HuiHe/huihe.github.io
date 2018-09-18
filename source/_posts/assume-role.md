---
title: aws sts assume-role
date: 2018-09-18 14:54:50
tags: aws
---

`aws sts assume-role` is very useful for cross-account access. Imaging using dev account for build and testing and assume to prod account for deployment.

To assume a role, your AWS account must be trusted by the role. The trust relationship is defined in the role's trust policy when the role is created. That trust policy states which accounts are allowed to delegate access to this account's role.

By default, the temporary security credentials created by AssumeRole last for one hour. However, you can use the optional DurationSeconds parameter to specify the duration of your session. You can provide a value from 900 seconds (15 minutes) up to the maximum session duration setting for the role. This setting can have a value from 1 hour to 12 hours.

To assume a role:

```sh
aws sts assume-role --role-arn arn:aws:iam::123456789012:role/xaccounts3access --role-session-name s3-access-example
```
The output of the command contains an access key, secret key, and session token that you can use to authenticate to AWS:

```json
{
    "AssumedRoleUser": {
        "AssumedRoleId": "AROA3XFRBF535PLBIFPI4:s3-access-example",
        "Arn": "arn:aws:sts::123456789012:assumed-role/xaccounts3access/s3-access-example"
    },
    "Credentials": {
        "SecretAccessKey": "9drTJvcXLB89EXAMPLELB8923FB892xMFI",
        "SessionToken": "AQoXdzELDDY//////////wEaoAK1wvxJY12r2IrDFT2IvAzTCn3zHoZ7YNtpiQLF0MqZye/qwjzP2iEXAMPLEbw/m3hsj8VBTkPORGvr9jM5sgP+w9IZWZnU+LWhmg+a5fDi2oTGUYcdg9uexQ4mtCHIHfi4citgqZTgco40Yqr4lIlo4V2b2Dyauk0eYFNebHtYlFVgAUj+7Indz3LU0aTWk1WKIjHmmMCIoTkyYp/k7kUG7moeEYKSitwQIi6Gjn+nyzM+PtoA3685ixzv0R7i5rjQi0YE0lf1oeie3bDiNHncmzosRM6SFiPzSvp6h/32xQuZsjcypmwsPSDtTPYcs0+YN/8BRi2/IcrxSpnWEXAMPLEXSDFTAQAM6Dl9zR0tXoybnlrZIwMLlMi1Kcgo5OytwU=",
        "Expiration": "2016-03-15T00:05:07Z",
        "AccessKeyId": "ASIAJEXAMPLEXEG2JICEA"
    }
}
```

Used in build bash scripts:

```sh
assume_role() {
  local creds
  $(aws sts assume-role --role-arn "$1" --role-session-name your-session-name --output text --query 'Credentials | join(``, [`"export AWS_ACCESS_KEY_ID="`,AccessKeyId,`" AWS_SECRET_ACCESS_KEY="`,SecretAccessKey,`" AWS_SESSION_TOKEN="`,SessionToken,`\n`])')
}

if [ -n "${ASSUME_ROLE:-}" ]; then
  assume_role "$ASSUME_ROLE"
fi
```

https://docs.aws.amazon.com/cli/latest/reference/sts/assume-role.html
