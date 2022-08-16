---
title: "Locals"
date: "2022-04-30 12:03:03"
---

Locals are used similar to variables, but are not part of a module its interface. They are often used to prevent repetition of values or to hold stateful values.

Locals are declared in the `locals` block and ideally in a separate `locals.tf` file.

```terraform
locals {
  retention_days = 60
}
```

Locals can be referenced in a module using `local.<local name>`.

Here we're creating a `aws_kms_key` and a `aws_cloudwatch_log_group` that both require a retention argument in days. To prevent maintaining the retention days in separate places we can use a local called e.g. `retention_days`.

```terraform
locals {
  retention_days = 60
}

resource "aws_kms_key" "example" {
  description             = "Example KMS key"
  deletion_window_in_days = local.prod_deletion_window_in_days
}

resource "aws_cloudwatch_log_group" "example" {
  name              = "Example CloudWatch Log Group"
  kms_key_id        = aws_kms_key.example.arn
  retention_in_days = local.retention_days
}
```

Locals can also be used to store stateful values, think of a local called `instance_ids` that stores the IDs of all dev and staging instances created.

```terraform
locals {
  instance_ids = concat(aws_instance.dev.*.id, aws_instance.staging.*.id)
}
```

Want to learn more about Locals? [Check out the docs](https://www.terraform.io/language/values/locals).

**Continue to [Outputs](../outputs)**
