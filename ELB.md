### ELB

> spread load, expose DNS handle failure, SSL termination, cookie stickiness, HA zones and separate public from private traffic.

AWS guarantees HA on the ELB and maintenance. 

### Three kind of ELBs: 
**Classic load balancer** is not recommended and then you have the v2 version which are application and network load balancers. You can setup private or public ELB. 

**Application load balancers** ALB are level 7 and they can handle multiple http apps even in the same machine, you can use the url or hostnames to balance. It is great for microservices, it support dynamic port mapping to run multiple containers on the same EC2 instance. The new app balancer is much cheaper because it can handle multiple apps. 
You can bundle multiple ec2 instances into target groups that are the same app/route. So you can scale and maintain cookie stickiness. 
You can enable stickiness at the app level transparent to the app.
ALB support HTTP/s and websockcets, classic load balancer does not support web sockets. 
The application servers doesn't see the IP of the client directly, it is in the X-Forwarded-For header set by the ELB. This is because the ELB does connection termination including SSL then redirects so the EC2 see the ELB ip, to get the client use the header.

**Network load balancers NLB** are level 4, lower level and are for TCP traffic. Really high performance and low latency. 
CLB/ALB both have ssl termination and healthchecks.
ALB is great for docker because it can route based on port and path
All ELBs have static host names, but not IPs, do not use IPs.
ELBs can scale but not instantaneously. NLBs see directly see the client IP, ALB use forward headers. 503 error means ELB is running out of capacity.

You can use auto scaling to automatically register new instances to the load balancer. Scale out is adding instances and scale in removing. You need to define auto scaling groups ASG and the balancer will use it to register new instances. 
ASG needs the same type of info as EC2 including AMI, EC2 user data, EBS volume, security groups, etc. You also need to specify min, desired and max capacity. You also need to specify the network and subnet settings, the load balancer info. and the scaling policies, that is when to scale in or out. This can be done using Cloudwatch which is the monitoring service in AWS, they do have alarms. so you can trigger scale in/out based on the triggers in the alarms. Some of the alarms can be based on avg cpu usage, number of request in the ELB, network usage, etc. You can also create custom metrics in cloud watch. Even you can scale based on a schedule. IAM roles attached to an ASG will be assigned to the EC2 instances. ASG is free, you pay for the instances. If you create ASG for you instances, with a min number if you terminate them, the AGS will provision a new one to meet the min req. ASG will terminate unhealthy instances. 

Load balancers and ASG are under the menu in EC2. First you need to create a launch template and then the ASG. The template is to create new EC2 instances, so the config is the same as for creating an EC2 instance, this way you enforce that all of them are the same type. When creating a ASG it is recommended that you go to advanced details and select load balancing so it works with the ELB, just select the target group previously created for the ELB. You can reuse the health check for ELB. You can attach and detach instances to the ASG, it is best practice that all ec2 instances are part of an ASG and ASG are part of target group for the ELB. So load balancers and ASG work together.
