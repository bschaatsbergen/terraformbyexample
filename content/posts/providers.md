---
title: "Providers"
date: "2022-04-28 12:00:00"
---

Terraform relies on providers to perform the actual work of provisioning resources. Each provider contains a set of resources and/or data sources that Terraform can manage.

The [Terraform Registry](https://registry.terraform.io/browse/providers) hosts publicly available Terraform providers. It's a good place to look at the documentation for a particular provider.

### Using the provider block

Every provider has a configuration block that is used to configure the provider.

```terraform
provider "aws" {
  region = "us-east-1"
}
```

```terraform
provider "google" {
  project = "my-project-id"
  region  = "us-central1"
}
```

Every provider has a set of arguments that are used to configure the provider, look up the respective provider documentation for more information.

**Continue to [Modules](../modules)**
