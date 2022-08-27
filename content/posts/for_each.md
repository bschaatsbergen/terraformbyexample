---
title: "For each"
date: "2022-08-24 17:26:00"
---
With the `for_each` argument you can create multiple instances for a particular resource.
The `for_each` argument either accepts a map or a set of strings, and creates an instance for each item in that map or set.
The `for_each` argument can be used in both modules and every resource type.


It's important to know that you can only use either `count` or `for_each` in a given resource.


#### Creating multiple resources using the for_each argument

Here we are creating 2 redis instances with different names

```terraform
resource "google_redis_instance" "set_example" {
  for_each       = toset(["special", "regular"])
  name           = "redis-instance-${each.key}"
  memory_size_gb = 10
}
```

Additionally, we can pass a map to the `for_each` argument and specify the size for each redis instance

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

It is also possible to pass a map of objects to the `for_each` argument

```terraform
resource "google_redis_instance" "map_with_objects_example" {
  for_each = {
    regular = {
      name = "regular-redis"
      size = 10
    }
    special = {
      name = "special-redis"
      size = 20
    }
  }

  name           = each.value.name
  memory_size_gb = each.value.size
}
```

#### Using the each.key
When you're using the `for_each` argument, the `each` object is available in the resource scope.
The `each.key` object represents the map key or set member of the current instance in the `for_each`.

#### Using the each.value

When you're using the `for_each` argument, the `each` object is available in the resource scope.
The `each.value` object represents the map value or set member of the current instance in the `for_each`.
In a set the `each.value` and `each.key` are the same.

Want to learn more about the for_each keyword? [Check out the docs](https://www.terraform.io/language/meta-arguments/for_each).

**Continue to [Dynamics](../dynamics)**
