# Cloud Lab 2 Submission: Load Balancer and Auto Scaling

* Student name: SAN Meyhieng
* Student ID: e20220677
* Learner Lab user name: SAN_MEYHIENG
* Date completed: 29 Oct 2026

## Security groups
![LoadBalancerSecurityGroup](images/01-sg-load-balancer.png)
![LaunchTemplateSecurityGroup](images/02-sg-launch-template.png)

## Target group
![Target group](images/03-target-group.png)
![Health checks](images/04-health-checks.png)

## Application Load Balancer
![Load balancer list](images/05-load-balancer-list.png)
![Load balancer details](images/06-load-balancer-details.png)

## Launch template
![Launch template](images/07-launch-template.png)

## Auto Scaling group
![ASG list](images/08-asg-list.png)
![ASG details](images/09-asg-details.png)

## Load balancing test
![Browser 1](images/10-browser-1.png)
![Browser 2](images/11-browser-2.png)

## Simulated application failure
![Stop httpd](images/12-stop-httpd.png)
![Target unhealthy](images/13-target-unhealthy.png)
![Target replaced](images/14-target-replaced.png)

About how many minutes passed between stopping `httpd` and the new instance becoming healthy? About XX minutes.

## Questions

1. **Why does the page show a different host name when you refresh it?**
   The load balancer spreads requests over the two healthy instances in the target group. Each instance writes its own host name in `index.html`, so the name changes depending on which instance answers.

2. **What did the health check test, and why did the instance fail it?**
   The health check sends an HTTP request to `/` on port 80 every 30 seconds and expects a 200 answer. After I stopped `httpd`, nothing was listening on port 80, so the request failed. After 2 failed checks in a row, the target was marked unhealthy, even though the EC2 instance was still running.

3. **Who replaced the failed instance?**
   The Auto Scaling group replaced it. The load balancer receives requests and forwards them to healthy targets. The target group holds the targets and runs the health checks. The Auto Scaling group has ELB health checks turned on, so it saw the unhealthy instance, terminated it, and launched a new one from the launch template to keep the desired capacity of 2.

4. **With desired 2, minimum 2 and maximum 3, how many instances run normally? When could there be 3?**
   Normally 2 instances run. There can be 3 for a short time while a failed instance is being replaced (the old one is still draining while the new one starts), or if the desired capacity is raised by a scaling policy or by hand. It can never go above the maximum of 3.

5. **How could the instances accept HTTP only from the load balancer?**
   In `LaunchTemplateSecurityGroup`, change the HTTP inbound rule source from Anywhere-IPv4 (0.0.0.0/0) to the security group `LoadBalancerSecurityGroup`. Then only traffic coming from the load balancer can reach port 80 on the instances.

## Problems and how I solved them
Screenshots 07 and 09 needed more than one view, because the AMI and instance type and the user data are on different tabs. I merged the captures for 07 and used the Integrations tab for the target group in 09.

## AI note
An AI tool suggested checking the Outbound rules of both security groups before launching, because the instances install Apache through user data and need outbound internet. I checked by opening the Outbound rules tab of each group, and both showed All traffic.

## Clean up
* `MyAutoScalingGroup` deleted and its instances terminated.
* `AutoScalingLaunchTemplate` deleted.
* `MyLoadBalancer` and `LoadBalancerTargetGroup` deleted.
* Both security groups deleted.
