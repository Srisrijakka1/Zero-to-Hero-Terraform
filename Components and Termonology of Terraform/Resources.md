<h1> Resources </h1>
<pre>
Each and every element in our Infrastructure is called as Resource
ex: vpc,subnets,ec2,s3,rds,...etc 
</pre>
<pre>
Example1:  Launch vpc in aws using terraform :


  resource "aws_vpc" "vpc_name"{
       cidr_block = "10.0.0.0/16"
       
       enable_dns_support = true
       enable_dns_hostnames = true

       tags = {
               Name = "MY VPC"
               "Purpose" = "Assignment"
       }
  }

</pre>

<pre>
Example2: Launch subnet in aws using terraform : 

  resource "aws_subnet" "private_subnet_name"{
      vpc_id = aws_vpc.vpc_name.id
      cidr_block = "10.0.1.0/24" 
      availability_zone = "ap-south-1a"
  }

</pre>

<pre>
Example3:  Launch private subnet in aws using terraform:

  resource "aws_subnet" "public_subnet_name" {
      vpc_id = aws_vpc.vpc_name.id 
      cidr_block = "10.0.2.0/24" 
      availability_zone = "ap-south-1a"
  }
</pre>

