---
title: "Hello world"
date: "2022-04-27 12:00:00"
---

As any other tutorial or course, we will print the classic "Hello World" message.

#### Before saying Hello

Ensure that you have Terraform installed and that you have the `terraform` command available. View [Download Terraform](https://www.terraform.io/downloads) for more information.


#### Saying Hello

Create the `hello.tf` file

```terraform
$ cat <<EOT >> hello.tf
resource "null_resource" "default" {
  provisioner "local-exec" {
    command = "echo 'Hello World'"
  }
}
EOT
```

Initialize and apply the changes using Terraform

```terraform
$ terraform init && terraform apply
```

The output should look like this

```terraform
Terraform will perform the following actions:

  # null_resource.default will be created
  + resource "null_resource" "default" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

null_resource.default: Creating...
null_resource.default: Provisioning with 'local-exec'...
null_resource.default (local-exec): Executing: ["/bin/sh" "-c" "echo 'Hello World'"]
null_resource.default (local-exec): Hello World
null_resource.default: Creation complete after 0s [id=2527848828031853855]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

Yahoo, "Hello World" is printed to the console.

**Continue to [State](../state)**
