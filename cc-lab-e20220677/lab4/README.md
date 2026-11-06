# Cloud Lab 4 Submission: Amazon VPC with Public and Private Subnets

* Student name: SAN Meyhieng
* Student ID: e20220677
* Learner Lab user name: SAN_MEYHIENG
* Date completed: 6 Nov 2026

## Part 1: VPC and internet gateway
![VPC](images/01-vpc.jpg)
![Internet gateway](images/02-internet-gateway.jpg)

## Part 2: Public subnet
![Public subnet](images/03-public-subnet.jpg)
![Public route table](images/04-public-route-table.jpg)
![EC2 in public subnet](images/05-ec2-public.jpg)
![Test public](images/06-test-public.jpg)

## Part 3: Private subnet
![Private subnet](images/07-private-subnet.jpg)
![NAT gateway](images/08-nat-gateway.jpg)
![Private route table](images/09-private-route-table.jpg)
![EC2 in private subnet](images/10-ec2-private.jpg)
![Test private](images/11-test-private.jpg)

## Problems and how I solved them
* The NAT gateway form offered a new "Regional" mode. I chose "Zonal" so the NAT gateway sits in lab4-public-subnet, as the lab describes.
* lab4-ec2-01 was launched with Amazon Linux 2023 instead of Amazon Linux 2. The command sudo yum update -y worked the same way.

## Clean up
* Both EC2 instances terminated.
* NAT gateway deleted and the Elastic IP released.
* Internet gateway detached and deleted.
* lab4-vpc deleted.
