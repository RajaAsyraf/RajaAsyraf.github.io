---
layout: post
title:  "Bug hunting on function in AWS Lambda with Serverless framework"
date:   2023-03-11 01:22:00 +0800
categories: bug hunting
---

This journey of bug fixing on AWS Lambda has been a tricky one, and there are a couple of lessons I would like to share. Before we go further, I'd like to mention that these tech stacks are new to me, and I am essentially learning by doing and tinkering around. Here is an overview of the systems I was working on, which involve the integration of:

1. AWS S3 bucket: A folder to receive the files to be processed.
2. AWS Lambda with the Serverless framework: To trigger service endpoints upon detecting a new file in AWS S3.
3. Processor Service: A service with endpoints exposed to Serverless, which are triggered to process the file.

![diagram-1-aws-lambda](/assets/aws-lambda.png)

I was working on adding another endpoint to be triggered by the existing Serverless function. The expectation was that once we placed a new file in the bucket, the Serverless function would trigger endpoint 1, followed by triggering endpoint 2. A retry mechanism is in place for that particular function. If an endpoint responds with an HTTP error, the function will attempt to trigger it again, up to 3 attempts.

Unfortunately, it didn’t work as expected. I ensured both endpoints worked correctly. The endpoint was triggered 3 times, and my first assumption was that the Serverless function did not receive a success response. However, that was not the case, and I spent quite some time trying different approaches in my code in the Processor Service to find any clues. I also monitored the logs in AWS Lambda, and after some time, I noticed a pattern where the Serverless function consistently stopped at 6.01 seconds.

I made a quick search on [StackOverflow][so-reference]{:target="_blank"} and found out that there is a default timeout of 6 seconds for the Serverless function. This explains why the function was stopping and proceeding with another attempt. To solve the issue, there are two options:

- Option 1 - Increase the Serverless function timeout.
- Option 2 - Reduce the execution time on the endpoints.

I went with option 2 because the endpoints can be optimized by utilizing synchronous operations in Node.js. Some operations that do not require any response should not be awaited.

I decided to document this because I had the opportunity to explore these tools with this use case. Additionally, I spent a couple of days thinking about this, and finally solving the issue was very satisfying and fun. I hope this documentation can be beneficial to others and myself in the future. Thank you for reading. Have a good day ahead.

[so-reference]: https://stackoverflow.com/questions/47594168/aws-lambda-task-timed-out-after-6-00-seconds
