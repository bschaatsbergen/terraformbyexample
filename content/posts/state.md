---
title: "State"
date: "2022-04-27 20:00:00"
---

Terraform uses the `state` to create plans and make changes to the infrastructure.
Terraform stores in the `state` the information about the managed infrastructure.
The `state` maps the real resources to the terraform configuration and metadata information.


By default, the state is stored locally in a file named `terraform.tfstate` but it can be stored remotely (e.g. `Google Storage Bucket`, or `S3`, or others), which allows better collaboration.


### Configuring the remote state

Example configuration for S3

```terraform
terraform {
  backend "s3" {
    bucket = "mybucket"
    key    = "path/to/my/key"
    region = "us-east-1"
  }
}
```

Example configuration for GCS

```terraform
terraform {
  backend "gcs" {
    bucket  = "tf-state-prod"
    prefix  = "terraform/state"
  }
}
```

### Inspecting and Modifying the state

* `teraform state list` lists all the resources managed by terraform
* `terraform import` - adds to the state resources that were created outside terraform
* `terraform state rm` - removes the resource from the state, tells terraform to "forget" about the resource
* `terraform state mv` - moves the resource inside the terraform state, this command is useful when attempting to rename a resource in terraform


Want to learn more about terraform State? [Check out the docs](https://www.terraform.io/language/state).

**Continue to [Providers](../providers)**

