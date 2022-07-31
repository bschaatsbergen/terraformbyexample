---
title: "Modules"
date: "2022-04-29 12:00:00"
---

Every `.tf` file in any directory is considered a module.

We can simply say that a module is a collection of Terraform files in a single directory. 

#### What is a module?

In practice we use modules to separate our Terraform code into logical parts. To either group or separate resources but also to prevent us from repeating ourselves.

Modules can be published to the [Terraform registry](https://registry.terraform.io/browse/modules) and used by other users.

#### Creating a module

A module can be as simple as a single `.tf` file. The variables that you declare in your module are the input variables that are passed to your module.

The below code is a module that creates a single Amazon S3 bucket with the name "example-bucket".

```terraform
resource "aws_s3_bucket" "default" {
  bucket = "example-bucket"
}

resource "aws_s3_bucket_acl" "default" {
  bucket = aws_s3_bucket.default.id
  acl    = "private"
}
```

#### Using a module

Calling a module is done by using the `module` block. Every module block requires a source argument that specifies the location of the module.

The `source` argument can either be the path to a local directory

```terraform
module "s3" {
  source = "path/to/s3-module"
}
```

or a URL to a remote module.

```terraform
module "s3" {
  source = "github.com/example/s3-module"
}
```

It's good to note that modules should be logical abstractions. To achieve that, we should use variables. In the next section we will learn how to use variables and how they can help us to create such a logical abstraction.

**Continue to [Variables](../variables)**
