---
title: Cloud Front
layout: default
---

# 3rd April 2025

Cloud front
Content delivery
what is cloud front
edge vs regional
distribution
console options
invalidation
ui options
logging
security options and origins
error pages and configure behaviour per page
continuous deployment
SSL certificate

Look into the difference bet.
General purpose and Directory bucket
for any service note:
number of AZ , Cost , Retrieval Cost

## Content Delivery
	- Network of interconnected servers that speeds up webpage loading for data heavy apps
	- CDN stands for content delivery network or content distribution network
	- If the user access the data from the server and the server is far from the user
		the data has to travel a long distance which can take time, and hence reduce 
		performance.
	- Instead the website data is stored on a CDN servers geographically closer to the user
		and reaches their computers much faster
		
## Advantages of CDN
	- Reduce page loading time
	- Reduce bandwidth costs
	- Increase content avaiability
	- Improve website security (Protects from DDoS)

## Cloud Front
	- It is a web service that speeds up the distribution of the static and dynamic web content.
	- CloudFront delivers your content through a world wide network of data centers called edge locations
	- When a user requests contents that we are serving with cloud front the request is routed to the 
		edge locations that provides the lowest latency so that content is delivered with the  best possible 
		performance.
		
	-If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately.
	
	- If the content is not in that edge location, 
		CloudFront retrieves it from an origin that you've defined—such as an Amazon S3 bucket,
		a MediaPackage channel, or an HTTP server (for example, a web server) that we have 
		identified as the source for the definitive version of your content.
		
	- CloudFront speeds up the distributions of our content by routing each user request
		through the AWS backbone network to the edge location that can best serve the content.
	
	- Using the AWS network dramatically reduces the number of networks that your users' 
		requests must pass through, which improves performance.
	
	- Users get lower latency—the time it takes to load the first byte of the file—and higher data transfer rates.
	
## What is Distribution?
	- A Configuration that tells CloudFront where to get content and how to deliver it globally,
		using a network of edge locations for fast and reliable content delivery.
		
## CloudFront configurations
	## Origin
	- S3
	- ELB
	- API Gateway
	- Mediastore container
	- MediaPackage container
	- VPC origins
	
	## origin path
	- To give specific folder access like /static
	- No other folder outside the /static is exposed
	
	## Enable Origin Shield
	- Adds a caching layer
	- Normally cloudfront edge locations pull content directly form the origin
	- With this option enabled cloudfront first checks a central cache before hitting the origin
	
	
	## Default cache behaviour
	
		## Path pattern
		- The path patterns determine which requests apply to this cache behaviour,
			based on the request's URI path
			
		## Viewer protocol policy
			## HTTP
			- Think of this as A sending postcard to B
			- Anyone who conveys the postcard has the access to read the content of the postcard
			- When user send request to the webserver, the server responds back 
				and the web browser displays the content
			
			## HTTPS
			- In this method the request is sent to the webpage server, the server sends
				SSL/TLS certificate to prove its trustworthy
			- Browser and the server agrees on a encryption method
			- browser sends the encrypted request 
			- The server responds with the encrypted data and the browser decrypts it

	## SSL
		- Secure sockets layer
		- protocol for encryting, securing, and authenticating communications that take place
			on the internet.
		- SSL was replaced by TLS some time ago, SSL is still a common used term for this technology
		
