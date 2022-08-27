---
title: "For each"
date: "2022-08-24 17:26:00"
---
With the `for_each` argument you can create multiple instances for a particular resource.
The `for_each` argument either accepts a map or a set of strings, and creates an instance for each item in that map or set.
The `for_each` argument can be used in both modules and every resource type.


It's important to know that you can only use either `count` or `for_each` in a given resource.


#### Creating multiple resources using the for_each argument

Here we are creating 2 Redis instances with different names

```terraform
resource "google_redis_instance" "set_example" {
  for_each       = toset(["special", "regular"])
  name           = "redis-instance-${each.key}"
  memory_size_gb = 10
}
```

Additionally, we can pass a map to the `for_each` argument and specify the size for each Redis instance using the `each` object.

```terraform
resource "google_redis_instance" "simple_map_example" {
  for_each = {
    regular = 10
    special = 20
  }

  name           = "redis-instance-${each.key}"
  memory_size_gb = each.value
}
```

#### The each object

In resources where the `for_each` argument is used, an `each` object becomes available.
This object has 2 attributes:

- `each.key` - Map key or set member corresponding to the current iteration.
- `each.value` - Map value corresponding to the current iteration. (If a set was provided, it would have the same value as the `each.key` has).

Want to learn more about the for_each argument? [Check out the docs](https://www.terraform.io/language/meta-arguments/for_each).

**Continue to [Dynamics](../dynamics)**
