---
title: "Data Sources"
date: "2022-09-18 20:24:00"
---

A `data source`, also known as `data resources`, allows Terraform to fetch and use information from resources defined outside Terraform or managed by a different
Terraform configuration.

A `data resource` also supports `count` and `for_each` arguments.

A `data resource` must be defined using a `data` block like the example below:

```terraform
data "aws_iam_role" "example" {
  name = "role_name"
}
```

#### Using Data sources to fetch information

Data sources can be used to fetch resources created by other Terraform configurations, like a VPC.
Here we are fetching a Google VPC, so we can use it to define a redis instance.

```terraform
data "google_compute_network" "redis-network" {
  name = "existing-vpc"
}

resource "google_redis_instance" "cache" {
  name           = "memory-cache"
  memory_size_gb = 1
  authorized_network = data.google_compute_network.redis-network.id
}
```

Data sources can also be used to fetch information not managed by Terraform,
 below is an example of a data source fetching an ubuntu AWS AMI, so we pass the AMI ID and create an ubuntu instance in AWS.

```terraform
data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["099720109477"] # Canonical account ID
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"

  tags = {
    Name = "MyWebInstance"
  }
}
```


Want to learn more about data sources? [Check out the docs](https://www.terraform.io/language/data-sources).
