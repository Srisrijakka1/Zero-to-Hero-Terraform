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

<pre>

  Example4: Launch your security group with allow only tcp traffic as in and allow all traffic to out:

  resource "aws_security_group" "security_group_name"{
    name = "Security group name"
    description = "Why you created this security group for .it is optional"

    ingress {
        from_port = 22
        to_port = 22
        protocol = "tcp"
        cidr_block = ["0.0.0.0/0"]
    }
  
    egress {
      from_port = 0
      to_port = 0
      protocol = "-1" 
      cidr_block = ["0.0.0.0/0"]
    }
  }
  
</pre>

<pre>
Example5: launch an ec2 server using terraform 

  resource "aws_instance" "ec2_instance_name"{
    ami = "ami-1234567"  #specify your desired ami-id
    instance-type = "t2.micro"
    subnet_id = aws_subnet.subnet_name.id 
    associate_public_ip_address = true  # Enable automatic public IP assignment  to access ec2 over direct connect.
    root_block_device {
        volume_type = "gp2"
        volume_size = 5
        delete_on_termination = true
      }
     tags = {
        "purpose" = "Assignment"
      }
  }
  
</pre>
