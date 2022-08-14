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

A module can be as simple as a single `.tf` file.

The below code is a module that creates an S3 bucket named "example-bucket".

```terraform
resource "aws_s3_bucket" "default" {
  bucket = "example-bucket"
}
```

#### Using a module

Calling a module is done by using the `module` block.

The `source` argument is required and can either be the path to a local directory

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

In the next section we will learn how to use variables and how they can help us to create logical abstractions from our Terraform modules.

Want to learn more about Modules? [Check out the docs](https://www.terraform.io/language/modules).

**Continue to [Variables](../variables)**
