---
title: "Variables"
date: "2022-04-30 12:03:00"
---

Terraform variables are used to control behavior of resources.
It's a common practice to declare an empty variable and set its value during execution.

> Variables can be set in many different ways (e.g., through a [.tfvars file](https://www.terraform.io/language/values/variables#variable-definitions-tfvars-files), [environment variables](https://www.terraform.io/language/values/variables#environment-variables), [command line flags](https://www.terraform.io/language/values/variables#variables-on-the-command-line), etc).

#### Declaring a variable:

```hcl
variable "max_instance_count" {
  type = number
}
```

#### Declaring a variable with a default value:

```hcl
variable "max_instance_count" {
  type = number
  default = 3
}
```

#### Declaring a variable with a default value and validation:

```hcl
variable "max_instance_count" {
  type = number
  default = 3

  validation {
    condition     = var.max_instance_count <= 5
    error_message = "max_instance_count is less than or equal to 5"
  }
}
```
