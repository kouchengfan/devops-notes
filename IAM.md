###IAM###

You need to select a region for all services besides IAM and S3

Root user is created with the account and should not be used.

IAM: User, Groups(teams, users) and Roles(machines). You apply permissions using policies in JSON to users, groups and roles. A policy has resources events and actions.

IAM Federation is using SAML standard to use your IAM solution for example LDAP active directory.

To log into EC2 instance use ec2-user@publlicIP  use -i and then pem file with the key, run chmod 0400 to give the right permissions to the pem file.

Use tag with key Name so you can add a name so it is show in the console.

Security groups are logical groups or firewall rules for the EC2 instances. Many to Many relation. Locked down to region. By default all inbound traffic is not allowed and all outbound allowed.
You can reference other security groups to extend functionality.

A elastic IP is a public IP that you own and never changes, you can use it to mask failure or if you need a constant IP but is is better to setup DNS names and use random IPs.
Use load balancer instead of setting IPs.

You get bill for elastic IPs.

Use EC2 user data field to execute programs during provisioning, so you can add your apps to run at bootstrap like installing Apache. Is used to bootstrap the instance and only runs once. Runs with root user. Click Advanced details and paste the script you want.

AMI are EC2 OS images, you have Amazon on linux based on Fedora, Red Hat, windows... you can create your own images and then create all your instances with them. You need this if you have proprietary software, extra security or federation is required to access your company LDAP.

Customs AMI are made for a specific region.

Instance names start with letters to give meaning: R -> RAM, G -> GPU, etc... M are the balanced ones and T the burstable, you have burst credits you can get in advance and if you get a spike, your CPU will burst and handle them until you run out. Credits are given as part of the instance and once used you recover them over time, you will never pay unless you do T2 unlimited. There is T2 unlimited which if you run out of credits then you will be charged.

Ec2 are billed per second
