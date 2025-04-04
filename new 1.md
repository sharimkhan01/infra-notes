---
title: EC2
layout: default
---
17-03-2025 l2-training

## User Data: It is possible to bootstrap(to run the command only
once the system boots), user data is used to achieve this task

EC2 user data is used to automate boot tasks such as:
	1. Installing updates
	2. Installing software
	3. Downloading common files from the internet
	4. Anything we can think of

Any command we run in user data runs with root (sudo) access


## Steps for Use case 1 (Use user data to install something on 
ec2 and check)

Step1: Launch ec2
Step2: Give necessary configs
Step3: Add the user data file
		#!/bin/bash
		sudo apt update
		sudo apt install apache2
		echo "Hello World"
Step4: Use http instead of https to launch the apache default page


## Create an Amazon EBS-backed AMI
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html#how-to-create-ebs-ami

https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/running-instance.png

## Steps to create an AMI for custom EC2
	1 – AMI #1: Start with an existing AMI
	2 – Launch instance from existing AMI
	3 – EC2 instance #1: Customize the instance
	4 – Create image (Instance powers down before creating 
		to ensure that everything on the instance is stopped
		and in consistent state during creation process)
	5 – AMI #2: New AMI
	6 – Launch instance from new AMI
	7 – EC2 instance #2: New instance
	
## to check EBS --> lsblk (list block)