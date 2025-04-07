7th April 2025

1. Provisioned concurrency configuration
	Use case in unreserved and reserved
2. Warm start in lambda
3. Types of invokation
4. sync vs async invocation
5. version vs alias
6. Explore API gateway

## How does lambda handler works 
	# Event-Driven Execution:
		- Lambda is an event-driven service, meaning your function is triggered by an event (e.g., a user request, 
			a file upload to S3, a message in a queue). 
	# Handler as the Entry Point:
		- When Lambda receives an event, it invokes the handler method you've configured. 
	# Input and Output:
		- The handler method receives an event object (containing the input data) and 
			a context object (providing information about the invocation, function, and execution environment). 
		- It can also optionally return a value, which is then returned to the caller. 
		
## How does aws-serverless-works
	# API Gateway Trigger:
		- When a client makes a request to your API Gateway endpoint, 
			it triggers the Lambda function associated with that endpoint.
	# Lambda Function:
		- The Lambda function, which uses aws-serverless-express, 
			receives the API Gateway event (request data).
	# Request Transformation:
		- aws-serverless-express converts the API Gateway event 
			into a standard Node.js HTTP request object.
	# Express App Execution:
		- The transformed request is then passed to your Express application, 
			which handles the request as if it were a regular HTTP request.
	# Response Transformation:
		- After your Express app processes the request and generates a response, 
			aws-serverless-express converts the Express response back into an API Gateway-compatible format.
	# API Gateway Response:
		- The transformed response is sent back to API Gateway, which then returns it to the client. 
		
## Difference between alias and version
	## [Medium article for the difference between alias and version](https://medium.com/@dalibor.plavcic/aws-lambda-versions-and-aliases-5f7a63a75afa)
		
## What is Concurrency?
	- The ability of the system to manage and execute multiple tasks or processes seemingly at the same time,
		either truly simultaneously or by rapid switching between them
	# With context to AWS
		- Concurrency is defined as the number of requests that your function is serving at any given time. 
		- When your function is invoked, Lambda allocates an instance of it to process the event. 
		- When the function code completes the execution, it can handle another request.

## AWS lambda concurrencies
	- [Medium article for AWS lambda concurrency](https://rajaswalavalkar.medium.com/aws-lambda-reserved-concurrency-v-s-provisioned-concurrency-scaling-db8e93703b02)
	- AWS provide us to configure the concurrency limits of our lambda functions to have better management on the multiple invocation as per your use case
	
	# Types of lambda concurrencies
		# Reserved concurrencies 
			- It guarantees the maximum number of concurrent instance for the function which can be invoked
			- When a function has being with a reserved concurrency configuration then no other lambda function within the same AWS account or region can use that concurrency.
			- There is no charge for configuring reservsed concurrency for a function.
			
			- If the function is invoked again while a request is still being processed, 
				then another instance is allocated, which increases the lambda function concurrency
			- The total concurrency limit which is defined by AWS for that specific region.
			
			## Advantage of Reserved concurrency
				# Other functions can’t prevent your function from scaling — 
					- All of your account’s functions in the same Region without reserved concurrency share the pool of unreserved concurrency 
						(Maximum Concurrency Limit). 
					- Without reserved concurrency, other functions can use up all of the available concurrency. 
					- This disables your function from scaling up in critical period. 
					- Thus defining the reserved concurrency will prevent this from happening.
				
				# Your function can’t scale out of control — 
					- Reserved concurrency also limits your function from using concurrency from the unreserved pool, which caps its maximum concurrency. 
					- You can reserve concurrency to prevent your function from using all the available concurrency in the Region, or from overloading downstream resources.				
					
		# Provisioned concurrencies
			- When a Lambda allocates an instance of your function, the runtime loads your function code and runs initialization code that you define outside of the handler
			- If code and dependencies are large, or we create SDK clients during init, this process can take some time.
			- When our function has not been used for some time, need to scale up, or when we update a fucntion,
				Lambda creates a new execution environment. This causes the portion of requests that are served by new instance to have higher latency than the rest, otherwise known as
				COLD START
				
			- By allocating provisioned concurrency before an increase in invocation, we can ensure that all request are served by initialized instances with low latency.
			- Lambda function configured with provisioned concurrency run with consistent start-up latency, making them ideal for building interactive mobile or web backends and latency sensitive microservices
			
			- Each version of a function can only have one provisioned concurrency config.
			- This cna be directed on the version itself or on an alias that points to the version.
			- Two alias can't allocate provisioned concurrency for the same version.
			
## Types of invocation in AWS lambda
	- [AWS official Blog](https://aws.amazon.com/blogs/architecture/understanding-the-different-ways-to-invoke-lambda-functions/)
	- 3 types:
		# Synchronous invocation
		# Asynchronous invocation
		# Event source mapping
		
	# Synchronous invocation
		- THe most straight forward way to invoke the lambda function.
		- Here the function executes immediately when we perform the lambda invoke api call.
		- This can be accomplised through a variety of options, including using CLI or any of the supported SDKs.
		
		- This invocation type flag specifies a value of RequestResponse .
		- This instructs AWS to execute the Lambda fucntion and wait for the function to complete.
		- When we use sync invoke, we are responsible for checking the response and determining if there was an error and if we
			should retry the invoke
		- There are list of services that can invoke a lambda function sync:
			1. ELB
			2. Amazon Alexa
			3. API gateway
			4. Cloudfront
			
	# Asynchronous invocation
		- The invocation type flag specifies EVENT.
		- If the function returns an error, AWS will automatically retry twice for a total of 3 invocation
		- List of services that invoke lambda async:
			1. S3
			2. SNS
			3. SES
			4. Cloudwatch logs
	
	# Poll based invokes (Constantly asks the resource or services if something is new ? Based on which it invokes the handler function)
		- This invocation model is designed to allow you to integrate with AWS stream and Queue based
			service with no code or server management.
		- Lambda will poll (regularly check for changes) the following services on your behalf, retrieve records, and invoke our functions.
		- List of supported services:
			1. Kenesis
			2. SQS
			3. Dynamo DB streams
			