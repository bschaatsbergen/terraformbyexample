---
title: "Conditionals"
date: "2022-08-01 19:25:00"
---

Infrastructure is often deployed using certain conditions, you might want to deploy a less nodes to development than to production or not deploy a certain resource at all.

Terraform provides a way to conditionally write resources using a ternary operator, the conditional expression is as following:

```terraform
condition ? value_if_true : value_if_false
```

#### Using a ternary operator to assign a value to a variable

Assign a value to a variable if a condition is true, otherwise assign a different value.

```terraform
variable "env" {
  type        = string
  description = "The environment to deploy to"

  validation {
    condition     = contains(["dev", "prod"], var.env)
    error_message = "Valid values are (dev, prod)."
  } 
}

resource "aws_elasticache_cluster" "example" {
  cluster_id           = "example-cluster"
  num_cache_nodes      = var.env == "prod" ? 6 : 3
  node_type            = "cache.m4.large"
  engine               = "redis"
  parameter_group_name = "default.redis3.2"
}
```

#### Using a ternary operator to optionally create resources

Conditionally deploy a Redis ElastiCache cluster to only the dev environment.

Here we are using the `count` argument to determine the number of times we should create this resource, if it's not a dev environment, we'll set the count to 0 and therefore not create the resource at all.

```terraform
variable "env" {
  type        = string
  description = "The environment to deploy to"

  validation {
    condition     = contains(["dev", "prod"], var.env)
    error_message = "Valid values are (dev, prod)."
  } 
}

resource "aws_elasticache_cluster" "example" {
  count = var.env == "dev" ? 1 : 0

  cluster_id           = "cluster-example"
  engine               = "redis"
  node_type            = "cache.m4.large"
  num_cache_nodes      = 3
  parameter_group_name = "default.redis3.2"
}
```

Want to learn more about Conditionals? [Check out the docs](https://www.terraform.io/language/expressions/conditionals).

**Continue to [For](../for)**
