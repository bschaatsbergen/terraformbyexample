---
title: "Splat"
date: "2022-09-14 19:26:00"
---

The [splat expression](https://www.terraform.io/language/expressions/splat) is a syntactic sugar variant of the [for expression](https://www.terraform.io/language/expressions/for), they produce the same result with the same input but are easier to declare.

For example, the following expressions are equivalent: `[for o in var.instances : o.name]` and `var.instances[*].name`.
If `var.instances` has an attribute `name`, both expressions return a list containing all the instance names.

It is important to note that the splat expression doesn't work with maps or objects.

#### Using a splat expression

It's a common practice to use splat expressions when defining [outputs](../outputs).

The following resource defines 2 Redis instances

```terraform
resource "google_redis_instance" "example" {
  count          = 2
  name           = "redis-instance-${count.index}"
  memory_size_gb = 10
}
```

We can use a splat expression to output all the names of all the Redis instances

```terraform
output "redis_instance_names" {
  value = google_redis_instance.example[*].name
}
```

Resources that use the `for_each` argument will appear in expressions as a map of objects, so you can't use splat expressions and you have to use a [for expression](../for) loop.

You can't refer to a resource using the splat operator `[*]` if the resource uses a `for_each` argument. This is because in this case the resource is a map of objects rather than a list of objects.
The splat operator applies only to lists.

Want to learn more about splat expressions? [Check out the docs](https://www.terraform.io/language/expressions/splat).
