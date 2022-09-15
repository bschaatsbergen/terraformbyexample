---
title: "Splat"
date: "2022-09-14 19:26:00"
---

A `splat expression` allows to define operations that could otherwise be achieved by a `for expression`.
It is important to note that the `splat expression` patterns do not work with map or objects. You have to use `for expressions` to achieve the same result.

For example, the following expressions are equivalent `[for o in var.instances : o.name]` and `var.instances[*].name`.
If `var.instances` has an attribute `name`, both expressions return a list containing all the instance names.


#### Using a splat expression

A more practical example is to use a `splat expression` when defining outputs.

The following resource defines 2 redis instances

```terraform
resource "google_redis_instance" "example" {
  count          = 2
  name           = "redis-instance-${count.index}"
  memory_size_gb = 10
}
```

We can use a `splat expression` to output all the names of the redis instances

```terraform
output "redis_names" {
  value = google_redis_instance.example[*].name
}
```

Resources that use the `for_each` argument will appear in expressions as a map of objects, so you can't use `splat expressions` and you have to use a [for expression](../for) loop.

Want to learn more about `splat expressions`? [Check out the docs](https://www.terraform.io/language/expressions/splat).
