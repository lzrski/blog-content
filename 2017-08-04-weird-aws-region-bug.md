I've been fighting a weird error coming from AWS SDK for Node.js:

    ConfigError: Missing region in config

I was setting the region like that:

```JavaScript
// Setup AWS SDK
const AWS = require('aws-sdk');

AWS.config.update({
  region: aws_region
});
```

Turns out that despite the fact that AWS is a singleton, it's config passed to service instances is not.

What is a *service instance*. E.g. this:

    new AWS.SQS()

In other words, SQS instance will have it's config baked in, and subsequent changes to AWS.config won't affect it.

So the order of execution is important. Consider:

    AWS.config.update({ region: A })
    const sqs = new AWS.SQS()
    AWS.config.update({ region: B })
    sqs.sendMessage(...) // the region from the sqs perspective is A!
