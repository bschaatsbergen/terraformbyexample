---
title: "Count"
date: "2022-08-01 19:24:00"
---

The `count` argument is used to determine the amount of instances to create for a particular resource. The `count` argument can be used in both a module as well as every resource type.

#### Creating multiple resources using the count argument

```terraform
resource "google_redis_instance" "example" {
  count          = 2
  name           = "redis-instance-${count.index}"
  memory_size_gb = 10
}
```

#### Using the count.index

When you're using the `count` argument, a `count` object becomes available in the resource scope. The `count.index` object represents the index of the current instance in the count. The index starts at 0, if you have a resource with a `count` of 4, the `count.index` object will be 0, 1, 2, and 3.

Want to learn more about the Count keyword? [Check out the docs](https://www.terraform.io/language/meta-arguments/count).

**Continue to [Conditionals](../conditionals)**
