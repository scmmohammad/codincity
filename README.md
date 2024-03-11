# codincity
Assessment

provider "aws" {
  region = "us-east-1"  
}
resource "aws_vpc" "my_vpc" {
  cidr_block           = "10.0.0.0/16"  
  enable_dns_hostnames = true
  tags = {
    Name = "MyVPC"
  }
}
resource "aws_internet_gateway" "my_igw" {
  vpc_id = aws_vpc.my_vpc.id

  tags = {
    Name = "MyIGW"
  }
}
resource "aws_route_table" "public_route_table" {
  vpc_id = aws_vpc.my_vpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.my_igw.id
  }

  tags = {
    Name = "PublicRouteTable"
  }
}
resource "aws_subnet" "public_subnet" {
  vpc_id     = aws_vpc.my_vpc.id
  cidr_block = "10.0.1.0/24"  
  availability_zone = "us-east-1a" 

  map_public_ip_on_launch = true

  tags = {
    Name = "PublicSubnet"
  }
}
resource "aws_route_table_association" "public_subnet_association" {
  subnet_id      = aws_subnet.public_subnet.id
  route_table_id = aws_route_table.public_route_table.id
}
