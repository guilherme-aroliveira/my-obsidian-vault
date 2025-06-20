Lambda <span style="color: #3588E9">--></span> is a Serverless Compute Service. It allows to run programs without having to worry about provisioning, maintaining, or waiting for service to be built.

One of the benefits is: automatically scales depending of the amount of user traffic. But there is a default limit of 1000 concurrent executions running at the same time. 

In some regions the reserved concurrency can be increase up to 3000, but only temporary. 

Reserve concurrency sets aside a certain number from the limit for a specific function <span style="color: #3588E9">--></span> it will decrease the number of unreserved concurrent functions available for the rest of the functions.

>[!note]
>On Lambda the user only pay for what he uses. There are no upfront costs, when there's no traffic, the user isn't charged. 

Lambda start with an event <span style="color: #3588E9">--></span> triggers Lambda to execute or invoke the provided code. The source can be  another AWS service such as S3 or API gateway, or it can be triggered from a stream of data or queues.

provision concurrency --> to avoid delay (execution latency) when starting a Lambda, it adds additional cost.

With provision concurrency, Lambda can be configured to keeps a certain number of functions running at all times and ready to execute. These functions stay initialized and ready to response in double-digit milliseconds.

Obs: A Lambda run can only run to 15 minutes maximum. And any function must adhere to a 10 GB RAM limit and a 10 GB storage limit.

When a function runs, Lambda automatically allocates a proportional amount of CPU power based of the amount of memory configured. If the amount of memory is increased, it's also automatically increasing the amount of CPU.  

<strong>Events Sources</strong>

Lambda supports Push and Pull Model for invoking the function.
- Push Model <span style="color: #3588E9">--></span> another service directly triggers Lambda and tells it to active when something happens.
- Pull Model <span style="color: #3588E9">--></span> information is flowing trough a stream or put into a queue that Lambda periodically pose and it goes into action when certain events are detected. 

The are two types for the Push Model: synchronous and asynchronous:
- synchronous <span style="color: #3588E9">--></span> Lambda returns the response back to the event source.
- asynchronous <span style="color: #3588E9">--></span> Lambda handles retry. After lambda is invoked by the source, it will first place the event into a queue and then immediately sends a success response back to the source. The success response only indicates that Lambda received the event and its working on it.

>[!note]
>In the Asynchronous Push Model it's important to include instructions in the code provided about how to handle retries and errors. 

If there's any errors, Lambda will attempt to run the code three times in total. There will be a one minute wait between the first and second attempt, and two-minutes before the second and third attempt. If the event still fails Lambda can be configured to send it to a dead letter queue. 

Lambda use destination to send information to another service about the results. It can have different destinations based on the code's result. 

>[!info]
>AWS automatically determines whether it will be synchronous or asynchronous based on which service is used to trigger Lambda.

Services that can be synchronous: CloudFormation, CloudFront, API Gateway and Cognito. Services that can be asynchronous: CloudWatch, EventBridge, S3 and SNS.

The are two types for the Pull Model: streams and queues:
- streams <span style="color: #3588E9">--></span> applications that have data that is continuously flowing at steady rate from one or sometimes many sources at the same time. Example: logging applications.
- queues <span style="color: #3588E9">--></span> applications that collect messages and place in a bucket or queue to be processed. Example: Amazon's Simple Queuing Service.

In case of errors or poor model invocation, for streams, Lambda will stop pulling when it retries the message, and for queues, Lambda will return the message to the queue. A dead letter queue can be configured to hold the expired messages after the maximum number of retries. 

<strong>Access Permissions</strong>

invocation permissions --> only needed for a push event source type. The event sources must have permission to trigger a Lambda function. This is done through an IAM resource policy. 

execution roles --> grants Lambda permissions to interact with other AWS service. Example: Lambda needs to place files into S3. It's done by placing two IAM policies in every execution role.
- IAM policy --> defines what Lambda is allowed to do with the other service.
- trust policy --> allows Lambda to assume the execution role and perform those actions on the other service.

>[!example] Example - IAM policy
>```json
>{
>  "Version": "2012-10-17"
>  "Statement": [
>    {
>      "Sid": "ExampleSourceFunctionArn",
>      "Effect": "Allow",
>      "Action": "s3:PutObect",
>      "Condition": {
>        "ArnEquals": {
>          "lambda:SourceFunctionArn": "arn:aws:lambda:us-east-1:account_ID:function:source_lambda"
>        }
>      }
>    }
>  ]
>}
>```

>[!example] Example - trust policy
>```json
>{
>  "Version": "2012-10-17"
>  "Statement": [
>    {
>      "Effect": "Allow",
>      "Principal": {
>        "Service": "lambda.amazonaws.com"
>      },
>      "Action": "sts:AssumeRole"
>    }
>  ]
>}
>```

<strong>Pricing model</strong>

Monthly Free Tier:
- 1 Million request and 400, 000 Gigabit seconds

Parts of Lambda Cost:
1. Number of Requests
2. Gigabit Seconds (Amount of Time x Amount of Resources)

A request begins each time Lambda starts executing the function in response to an event trigger. 

For the amount if time, the clock start when the code begins executing and ends when it terminates. It includes and any initialization or shutdown phase in the Lambda function code. 

The price for the amount of time will depend on the amount of memory allocated to the function. Any amount of memory from 128 megabytes to 10 gigabytes can be allocated. 

The type of processor configured has an impact on pricing. Ephemeral storage and provisioned concurrency also add additional cost to the Lambda functions --> the cost is region-specific.

<strong>Functions</strong>

A function handler must be included to make the code work with Lambda. The function handler contains two objects: event object and context object.
- event object <span style="color: #3588E9">--></span> give the event source an opportunity to pass information onto the Lambda function. Example: pass along information about the S3 bucket (event source).
- context object <span style="color: #3588E9">--></span> generated by AWS and includes information specific to the runtime environment. It allows the code to communicate with the runtime environment within the function.

>[!info]
>The context object will vary dependent on which programming language is being used. 

>[!example] Additional info
>AWS Lambda Developers Guide
>https://docs.aws.amazon.com/lambda/latest/dg/welcome.html
>
>Best Practices:
>https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html

Creating a Basic Lambda Function with AWS CLI:

>[!example] Lambda Function
>```python
>def lambda_handler(event, context):
>  if event["name"] == "KodeKloud":
>    return "Successful" 
>```
>---
>```shell
>aws lambda create-function \ 
>--function-name "basichelloworld" \ 
>--runtime "python3.7" \
>--zip-file "fileb://basichelloworld.zip" \
>--handler "basichelloworld.lambda_handler" \
>--role "arn:aws:iam:ID:role/LambdaDemoRole"
>```
>Obs: The AWS CLI must be installed on the operating system.

To test the function using CLI:

```shell
aws lambda invoke --function-name my-function --payload '{"name":"KodeKloud"}' --cli-binary-format raw-in-base64-out output.txt
```

Creating a Canary Function using Blueprint:
- create function on the AWS console
- select "Use a blueprint" option
- search for the canary blueprint
- configure the Destination

>[!note]
>Canaries are basically scripts that allow to test the availability of endpoints, APIs, or websites.

Lambda can configured to periodically pull queues from SQS to relay messages. Then Lambda will invoke a function if a message is retrieved --> Pull Invocation type.

Create SQS Function:
- select "Use a blueprint" option
- search for SQS queue blueprint
- configure the SQS trigger  

>[!info]
>In the Pull Invocation type, a new role for the policy templates must be created, because AWS Lambda needs permission to pull sqs queues. 

<strong>Monitoring</strong>

Lambda integrates with AWS CloudWatch and X-ray services to provided a variety if monitoring and troubleshooting features. 

CloudWatch automatically integrates with Lambda to monitor the number of invocations or requests, the duration per request and the number of requests resulting to error.

Additional Metrics can be added though the CloudWatch dashboard which includes: 
- throttle due to concurrent limit
- the amount of Delay pulling data from stream sources refereed to as "Iterator Age"
- number of event in dead letter queue
- detailed concurrent executions metrics

Lambda Insights --> additional monitoring extension that can be enabled with CloudWatch to provide additional monitoring features, such as aggregate metrics about the functions behaviors. 

AWS X-Ray --> monitoring and troubleshooting tool that provides a visual mapping and allows to view requests as they through the application. 
- identify performance bottlenecks and errors. 
- trace Lambda function path

Flow Logs --> monitoring tool that provide information for the traffic inside the VPC> It can show information about TCP/IP and IP packet data information. But they are not available default for Lambda.

<strong>Lambda Networking</strong>

When a Lambda function is created, it's placed into a special area of AWS called a services VPC --> managed and maintained by AWS.

The default VPC Lambda services VPC already has access to the internet, and it also has access to all of the other AWS services --> network connectivity for Lambda doesn't need to be set up.

>[!note]
>Lambda Services VPC that contains all of the functions cannot communicate with the private VPC or any of the resources inside of them such as EC2 instance or database service. 

The are two option for adding networking for Lambda:
- run Lambda inside the private VPC 
- leave Lambda in the Lambda services VPC but add a private connection between the private VPC and Lambda using an interface endpoint. 

To run Lambda inside the private VPC, just select it on the advanced configuration option in the Lambda settings --> the downside is that the user is responsible for high availability (Lambda must run in more than 1 availability zone).

To have access to the internet a NAT gateway must be added to each availability zone that's being used by the Lambda inside the private VPC --> outbound internet connectivity

To have connectivity to other AWS service that are not inside the VPC, endpoints from the VPC to the other AWS service must be added --> it will add costs and affect the number of concurrent Lambda executions.

>[!info]
>Each time a Lambda function is run in the private VPC, it creates a new internet interface called an ENI (Elastic Network Interface) --> is attached to Lambda and allows it to communicate using TCP/IP.

Obs: Any Lambda executions above the ENI limit will be throttled.

--> Using the second networking option for Lambda, the concurrent executions will not be limited by the number of ENIs in the VPC, but there will be an additional cost for the interface endpoint connection. 

>[!example] Example - Default Lambda
>- create endpoint on VPC endpoints 
>- select the Lambda option on Services 
>- select the VPC for the endpoint
>- select the subnets

<strong>Lambda Containers</strong>

Lambda stays serverless event when running containers, and there's the automatic scaling that Lambda providers. 

Lambda will scale up to thousands of executions of the container if needed, or all the way down to zero if there is no traffic. 

On Lambda users can run containers up to 10 gigabytes on size.

To use containers with lambda:
- add some code to the container
- add the container app

>[!example]
>```python
>import sys
>def handler(event, context):
>  return 'Hello form Kodekloud with AWS Lambda using Python' + sys.version + '!'
>```
>---
>```Dockerfile
>FROM public.ecr.aws/lambda/python:3.8
>
>COPY requirements.txt
>RUN pip3 install -r requirements.txt --target "$(LAMBDA_TASK_ROOT)"
>
>COPY app.py ${LAMBDA_TASK_ROOT}
>CMD ["app.handler"]
>```