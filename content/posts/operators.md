---
title: "Operators"
date: "2022-07-31 21:25:00"
---

In Terraform it's common to use operators to implement validation logic.

#### Equality operator

Equality operators take two values and produces a boolean value.

```terraform
variable "user_count" {
  type        = number
  description = "Amount of users"

  validation {
    condition     = var.user_count != 1"
    error_message = "User count cannot be 1"
  }
}
```

#### Comparison operator

Comparison operators take two numbers and produces a boolean value.

```terraform
variable "user_count" {
  type        = number
  description = "Amount of users"

  validation {
    condition     = var.user_count >= 1"
    error_message = "User count must be at least 1"
  }
}
```

#### Logical operator

Logical operators are often used to chain operators.

```terraform
variable "user_count" {
  type        = number
  description = "Amount of users"

  validation {
    condition     = var.user_count >= 1 && var.user_count <= 100"
    error_message = "User count must be between 1 and 100"
  }
}
```

Want to learn more about Operators? [Check out the docs](https://www.terraform.io/language/expressions/operators).

**Continue to [Count](../count)**
