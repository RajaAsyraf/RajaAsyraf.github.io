---
layout: post
title:  "Bug hunting on function in AWS Lambda with Serverless framework"
date:   2023-03-11 01:22:00 +0800
categories: bug hunting
---

This journey of bug fixing on AWS Lambda is a tricky one and there are a couple of lessons I would like to share. Before we go further, these tech stacks are new to me and basically this is how learn by doing and tinkering around. An overview of the systems that I was working on with integration of:

1. AWS S3 bucket - a folder to receive the file to be processed
2. AWS Lambda with Serverless framework - to trigger service endpoints upon detecting new file in AWS S3
3. api-processor - a service with endpoints exposed to Serverless to be triggered and processing the file.

I was working to add another endpoint to be triggered on the existing Serverless function. The expectation is once we place a new file in the bucket, the Serverless will trigger endpoint 1 and follow with triggering endpoint 2. There is a retry-mechanisms in place in that particular function. Let’s say if the endpoint responds with http error, the function will do another attempt to trigger again up until 3 attempts. 

Unfortunately it doesn’t work as expected. I have ensured both of these endpoints work as expected. The endpoint was triggered 3 times and my first assumption was maybe the Serverless did not get a success response. But that’s not the case, and I spent quite some time trying different ways in my code in the api-processor to see any clues. I also monitor the logs in AWS Lambda and after quite some time, I noticed the same pattern where the Serverless function stopped at 6.01 seconds.

I made a quick search on [StackOverflow][so-reference]{:target="_blank"}, and found out that there is a default timeout of 6 seconds in the Serverless function. This clears everything on why the function was stopped and proceeds with another attempt. So to solve the issue, there are 2 options:
- Option 1 - Increase the Serverless function timeout.
- Option 2 - Reduce the execution time on the endpoints.

I went with option 2 because the endpoints can be optimized by utilizing the synchronous operations in Node.js. Some operations that do not require any response should not be awaited.

I decided to document this because I had the opportunity to explore these tools with this use case. Besides that, I spent couple of days thinking about this and finally get to solve that issue is very satisfying and fun. I hope this can be beneficial to others and myself in the future. Thank you for reading. Have a good day ahead.

[so-reference]: https://stackoverflow.com/questions/47594168/aws-lambda-task-timed-out-after-6-00-seconds







