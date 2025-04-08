---
title: S3_Lambda
layout: default
---

4th April 2025

# SSL
# Continuous Deployemnt
# Can you access glacier data instantly?
# Multipart uploads
# Explore on IAM, a high level idea
# s3 express one zone
# What is Lambda?
# Lambda UI options (brief idea on each)
# How is lambda different from an ec2 instance?
# Lambda runtimes, lifecycles
# Lambda layers

## SSL
	- To understand SSL goto [Internet Society](https://www.internetsociety.org/deploy360/tls/basics/?gad_source=1&gclid=CjwKCAjw47i_BhBTEiwAaJfPpglZsxbW0FZQwa4snQzS9Sr148nsDlBuuwIXfvMD9GWjA-nxxWU5PBoCJ9AQAvD_BwE)
	
## Continuous Deployemnt
	- [Continuous Deployemnt](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/continuous-deployment.html)

## Can you access glacier data instantly?
	- Yes we can and we cannot
	- Depends on the class of S3 Glacier
	- Check about the classes [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/glacier-storage-classes.html)
	- General idea and use cases [here](https://aws.amazon.com/s3/storage-classes/glacier/)

## Multipart uploads
	- Multipart uploads allows you to upload a single object to amazon s3 as a set of parts
	- Each part is a contiguous portion of the object's data.
	- You can upload these object parts independently and in any order.
	- For uploads your updated aws client automatically calculates the checksum of the object
		and sends the data to the amazon s3 along with the size of the object as a part of the request.
	- If the transmission of any part fails, you can retransmit that part without affecting the other parts.
	- After all the parts are uploaded, S3 assembles them to create the object.
	- Used for files of size greater or equal to 100MB

## AWS Lambda
	- Lambda runs our code on a high-avaiability computer infra and performs all of the administration of the compute
		resources, including server and os maintainence, capacity provisioning and automatic scaling and logging
	- With lambda all we need to do is provide code in one of the language runtime that Lambda supports

	- We organise our code into lambda functions.
	- The lambda service runs your function only when needed and scales automatically.
	- We only pay for the compute time that you consume
	- No charge when code is not running
	
	
## Difference between AWS EC2 and AWS Lambda
	## Management
	- User manages all the aspects of provisioning, deployement and operation
	
	- In Lambda user only provides code to the service
	- AWS handles all the aspects of infra
	
	## Price
	- Monthly/ Hourly cost varies depending on VM type and size
	- User billed monthly
	
	- In Lambda, it is pay per execution and compute time used for those execution
	
	## Performance
	- EC2
		- Instance runs until it is deliberately stopped
		- App in the instance is immediately available and running
		
	- Lambda
		- Always available but only runs when executed
		- Upto 100ms delay before code is loaded and executed (cold start)
		- Runtime limited to 15 mins and cannot use more than 3008 MB
	
	## security
	- EC2
		- User is responsible for instance and application security
		- additional aws service may be needed to implement proper ec2 security
	- Lambda
		- Users can employ IAM role permissions for Lambda
		- The underlying infra is secured by AWS
	
	## Scaling
	-EC2
		- User is responsible for scaling but can use services as EC2 auto scaling groups
	- Lambda
		- Scales dynamically in response to traffic and automatically adjusts the number of concurrently
			executing functions.
	
