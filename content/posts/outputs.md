---
title: "Outputs"
date: "2022-07-31 21:19:00"
---

Terraform output values can be seen as return values of resources. They are part of a module its interface.

#### Declaring an output value

Each output must be declared using an output block.

```terraform
output "example_compute_instance_name" {
  value = google_compute_instance.example.name
}
```


#### Declaring an output value with a description

As output values are part of the interface you can add a description to them.

```terraform
output "example_compute_instance_name" {
  value       = google_compute_instance.example.name
  description = "The name of the example compute instance"
}
```

#### Declaring a sensitive output value

Sensitive values are masked in the output of `terraform plan` and `terraform apply`.

> Note: Terraform will persist the value to the state file as cleartext, anyone that can view the state file can see the value.

```terraform
output "sql_database_root_password" {
  value       = google_sql_database_instance.example.root_password
  description = "The initial root password"
  sensitive   = true
}
```

#### Using an output value in a module

Output values can be used using the format `module.<module name>.<output value>`.

```terraform
module "compute_instance" {
  source = "path/to/compute_instance_module"
  ... additional module configuration ...
}

resource "google_compute_instance_iam_member" "member" {
  instance_name = module.compute_instance.name
  role          = "roles/compute.osAdminLogin"
  member        = "user:bruno@example.com"
}
```

Want to learn more about Outputs? [Check out the docs](https://www.terraform.io/language/values/outputs).

**Continue to [Operators](../operators)**
