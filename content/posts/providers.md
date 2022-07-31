---
title: "Providers"
date: "2022-04-28 12:00:00"
---

Terraform relies on providers to perform the actual work of provisioning resources. Each provider contains a set of resources and/or data sources that Terraform can manage.

The [Terraform Registry](https://registry.terraform.io/browse/providers) hosts publicly available Terraform providers. It's a good place to look at the documentation for a particular provider.

### Using the provider block

Every provider has a configuration block that is used to configure the provider. It's common to create a `provider.tf` file to manage this configuration.

```terraform
provider "aws" {
  region = "us-east-1"
}
```

### Using the provider block together with the Terraform block

Providers are often constrained to a range of Terraform versions. This allows you to specify the version range of the provider that's compatible with the version of your Terraform installation.

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}
```

**Continue to [Modules](../modules)**
