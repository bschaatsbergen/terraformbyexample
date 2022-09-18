---
title: "State"
date: "2022-04-27 20:00:00"
---

Terraform uses [state](https://www.terraform.io/language/state) to create plans and make changes to your resources.


Terraform stores state about the resources that it creates for you.
The state is stored in so called state files, by default these files are called `terraform.tfstate` files.
The state file can be seen as mapping between the resources created on the cloud provider side and the resources declared in your Terraform files.


By default, the state is stored locally in the file named `terraform.tfstate`, but it can also be hosted remotely (e.g. in a Google Cloud Storage Bucket, an Amazon S3 bucket, or others).
This is typically done so that teams can collaboratively make changes against the remote hosted `terraform.tfstate` file.

If you want to store your state remotely, you'll need to setup a [remote backend](https://www.terraform.io/language/settings/backends/configuration#backend-configuration).

### Storing the Terraform state in S3

It's a common practice to create this file in a `backend.tf`.

```terraform
terraform {
  backend "s3" {
    bucket  = "my-terraform-state-bucket"
    key     = "path/to/my/key"
    region  = "us-east-1"
    encrypt = true
  }
}
```

### Storing the Terraform state in a Cloud Storage Bucket

It's a common practice to create this file in a `backend.tf`.

```terraform
terraform {
  backend "gcs" {
    bucket  = "my-terraform-state-bucket"
    prefix  = "path/to/my/key"
  }
}
```

### Perform operations on your Terraform state

Terraform allows us to perform various operations on our Terraform state.
Think of importing manual created objects into the Terraform state, or removing a resource from the Terraform state file.

See below for a list of commands that are available to perform various operations on your Terraform state.

* `teraform state list` lists all the resources managed by terraform
* `terraform import` - adds to the state resources that were created outside terraform
* `terraform state rm` - removes the resource from the state, tells terraform to "forget" about the resource
* `terraform state mv` - moves the resource inside the terraform state, this command is useful when attempting to rename a resource in terraform


Want to learn more about Terraform State? [Check out the docs](https://www.terraform.io/language/state).

**Continue to [Providers](../providers)**

