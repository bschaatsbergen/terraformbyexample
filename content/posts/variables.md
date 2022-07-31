---
title: "Variables"
date: "2022-04-30 12:03:00"
---

Terraform variables are used to control behavior of resources.
It's a common practice to declare an empty variable and set its value during execution.

> Variables can be set in many different ways (e.g., through a [.tfvars file](https://www.terraform.io/language/values/variables#variable-definitions-tfvars-files), [environment variables](https://www.terraform.io/language/values/variables#environment-variables), [command line flags](https://www.terraform.io/language/values/variables#variables-on-the-command-line), etc).

It's a common practice to declare your variables in a separate `vars.tf` file.

#### Declaring a variable

```terraform
variable "max_instance_count" {
  type = number
}
```

#### Declaring a variable with a default value

If a default value is present, the variables is considered to be optional and the default value will be used if no value is set.

```terraform
variable "max_instance_count" {
  type = number
  default = 3
```

#### Declaring a variable with a default value and validation

You can create validation rules for a variable by adding a validation block.

```terraform
variable "max_instance_count" {
  type = number
  default = 3

  validation {
    condition     = var.max_instance_count <= 5
    error_message = "max_instance_count should be less than or equal to 5!"
  }
}
```

#### Using a variable in a module

To use a variable in a module, you need to use `var.<variable name>`

```terraform
variable "bucket_name" {
  type        = string
  description = "The name of the S3 bucket"
}

resource "aws_s3_bucket" "default" {
  bucket = var.bucket_name
}
```

#### Calling a module using input variables

Variables act as input variables for a module, this allows other users to set their own values for a variable.

```terraform
module "s3" {
  source = "path/to/s3-module"
  bucket_name = "my-bucket"
}
```
