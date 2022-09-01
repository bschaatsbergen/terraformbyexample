---
title: "Dynamics"
date: "2022-08-31 19:24:00"
---

The `dynamics` expression is used to produce nested blocks inside the resource it is defined.
The `dynamics` expression acts as a `for` expression but produces nested blocks instead.

It is important to note that a `dynamic` block can not be used to generate the meta-argument blocks such as `lifecycle` and `provisioner` blocks, since Terraform needs to process the meta-arguments before evaluating expressions.


#### Creating a Firewall rule defining multiple allow blocks

```terraform
resource "google_compute_firewall" "default" {
  name    = "example-firewall"
  network = google_compute_network.default.name

  allow {
    protocol = "tcp"
    ports    = ["80", "8080", "1000-2000"]
  }
  
  allow {
    protocol = "udp"
    ports = ["3000-4000"]
  }
  
  source_tags = ["example"]
}
```

#### Creating Firewall rule using the dynamics expression

```terraform
resource "google_compute_firewall" "default" {
  name    = "example-firewall"
  network = google_compute_network.default.name

  dynamic "allow" {
    for_each = {
      tcp = ["80", "8080", "1000-2000"]
      udp = ["3000-4000"]
    }
    content {
      protocol = allow.key
      ports    = allow.value
    }
  }
  source_tags = ["example"]
}
```

The label of the `dynamic` block, `"allow"` in the example above, defines what kind of nested block to create.

#### The iterator object

The iterator object, `allow` in the example above has 2 attributes:
This object has 2 attributes:

- `key` - Map key or set member corresponding to the current iteration.
- `value` - Map value corresponding to the current iteration. (If a set was provided, it would have the same value as the `each.key` has).

Want to learn more about the Dynamics expression? [Check out the docs](https://www.terraform.io/language/expressions/dynamic-blocks).
