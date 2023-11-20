# Highly-Available-Multi-Tier-Web-Application
Specifically, we will walk through the following topics`:
1. Network – Amazon VPC
2. Compute – Amazon EC2
3. Database – Amazon Aurora
4. Storage – Amazon S3
5. Clean up resource.

A. Network - Amazon VPC -
   In this lab, we'll create not only one Public Subnet and one Private Subnet in two Availability Zone(AZ-a, AZ-c) but also one NAT Gateway placed on the Public Subnet through VPC Wizard. After configuring these resources, you will set up a routing table to define the network traffic flow. Through these tasks, you can complete a basic networking configuration to create a highly available and scalable web service environment. 

Network Architecture - 
   
<img width="552" alt="network architecture" src="https://github.com/manas0120/Highly-Available-Multi-Tier-Web-Application/assets/60257363/8d22459a-3bd4-4fea-8d05-9d0805903c47">

1.) Create  VPC - Amazon Virtual Private Cloud (Amazon VPC) allows you to start AWS resources with a user-defined virtual network. This virtual network, along with the benefits of using AWS's scalable infrastructure, is very similar to the existing network operating in the customer's own data center. 

a. After logging in to the AWS console, select VPC from the service menu. 

Select VPC Dashboard and click Launch VPC Wizard to create your own VPC. 

To create a space to provision AWS resources used in this lab, we will create a VPC and Subnets. Select VPC, subnets, etc in Resource to create tab and change name tag to VPC-Lab. Leave the default setting for IPv4 CIDR block. 

To design high availability architecture, we create 2 subnet space and select 2a and 2c for Customize AZs. And set the CIDR value of the public subnet that can communicate directly with the Internet as shown in the screen below. Set the CIDR value of the private subnet as shown in the screen. 

You can use a NAT gateway so that instances in your private subnets can connect to services outside your VPC, but external services cannot initiate direct connections to these instances. In this lab, we will create a NAT gateway in only one Availability Zone to save cost. Also, for DNS options, enable both DNS hostnames and DNS resolution. After confirming the setting value, click the Create VPC button. 

As the VPC is created, you can see the process of creating network-related resources as shown in the screen below. For NAT Gateway, provisioning may take longer compared to other resources. 

You can check the information of the created VPC. Check related information such as CIDR value, route table, network ACL, etc. Check that the values you just set are correct. 

2.) Create VPC Endpoint - In this section, you create an endpoint for S3 to learn a VPC endpoint. 

In VPC Dashboard, select Endpoints. Click Create endpoint button. 

Type s3 endpoint for name and select AWS services in Service category tab. In the search bar below, type s3 and select the list at the top. 

For S3 VPC endpoints, there are gateway types and interface types. For this lab, select the gateway type. And for the deployment location, select the VPC-Lab-vpc created in this lab. 

Choose a route table to reflect the endpoint. Select the two private subnets as shown below. Additional routing information for using the endpoint is automatically added to the selected route table. 

  
NOTE:- VPC endpoints are communications within the AWS network and have the security and compliance advantage of being able to control traffic through the endpoints. You can also optimize the data processing cost if you transfer your data through a VPC endpoint rather than a NAT gateway. 


B. Compute - Amazon EC2
   Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. Amazon EC2’s simple web service interface allows you to obtain and configure capacity with minimal friction. It provides you with complete control of your computing resources and lets you run on Amazon’s proven computing environment.


EC2 Architecture - Auto Scaling Group to deploy web service instances to private subnets in VPC that we created earlier in this network lab. This configures the highly available web services so that external users can access the Sample Web Page through the web.

   <img width="554" alt="EC2 Architecture" src="https://github.com/manas0120/Highly-Available-Multi-Tier-Web-Application/assets/60257363/05c12a41-1634-4b3c-a2c8-577a1306d72e">
