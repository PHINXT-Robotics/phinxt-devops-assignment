## Introduction

This is an exercise used to assess your approach to development and use of
infrastructure as code tooling. This has been tested using terraform v0.14.5 we advise you use 
this version.

Here we have some terraform to build a simple VPC network, for now we have just one instance running the web server 
Nginx in its default configuration, serving up the default welcome page. To run this use the following command:

```shell
terraform init && terraform apply -var-file=dublin.tfvars
```

Your task is to update the project as detailed below. 
After completing each stage, a test to show the things are still working can be performed by running the following command. At each step, you should be able to see the Nginx welcome 
page HTML.

```shell
terraform output nginx_domain | xargs curl
```

## The steps

1. We want to be able to run the same stack in the US. Please build the 
   same stack in the us-east-1 (Virginia) region, without removing the one 
   currently in place.  Feel free to modify the code and or structure 
   as much as needed in order to achieve this; you will need to consider 
   the terraform state, as each stack should have its own state, however, 
   you don't need to go as far as setting up a remote state. As for a CIDR,
   the new VPC use whatever you feel like, providing that it is compliant
   with RFC-1918 and that it does not overlap with the Dublin network.

1. The Virginia region has several availability zones and we want to use 4 
   of them, however, we still want to run the stack in Ireland using the 3 
   availability zones there. Modify the Virginia stack to span 4 
   availability zones. You can approach this as you prefer, but you should 
   make the code as reusable as possible.

1. The EC2 instance running Nginx went down over the weekend and caused an
   outage, hence we need a solution that is more resilient than just a 
   single instance. Please implement a solution that would continue to 
   run in the event where one of the instances goes down. 

1. We want to improve the security and segregation of our network, so
   we have decided that we would like private subnets that are not 
   addressable on the internet. Modify the VPC to meet this requirement,
   while ensuring that the private subnets still have egress internet
   connectivity.

1. In order to provide a consistent environment on the teams CI server and
   each engineer's workstation we have decided that it would make sense to
   run terraform in Docker. Create a Dockerfile and a wrapper script that
   will enable this. THe script should be callable with the same arguments
   as the terraform cli tool (e.g. init/plan/apply)

## Delivering your solution
To send us your solution, you can fork this repo and then send us the link to your modified version.

Good luck!

 

