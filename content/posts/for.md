---
title: "For"
date: "2022-08-01 19:26:00"
---

With `for` loops you can iterate through a list, a set, a tuple, a map, or an object.

`for` loops can produce different results depending on how they are declared, the type of brackets decide the result type.

It's important to know that `for` loops are used to manipulate and transform values and **not** delegate the creation of N instances of a resource - we use the `count` or `for_each` argument to achieve that.

#### Declaring a for loop that produces a tuple

Here we're storing the `names` coming from a data source into a local named `regions` using a `for` loop.

```terraform
data "aws_regions" "available" {}

locals {
  regions = [for name in data.aws_regions.available.names : name]
}
````

Optionally we could extract the index from the `for` loop using a second symbol right after the `for` keyword.

```terraform
data "aws_regions" "available" {}

locals {
  regions_indices = [for index, name in data.aws_regions.available.names : index]
}
```

In the above example, `regions_indices` its value is a tuple containing the indices (0, 1, 2, etc) of the region names.

#### Declaring a for loop that produces an object

If we use curly braces to annotate our `for` loop, we produce an object. When producing an object we must provide an additional expression using `=>`, this constructs the values of the object for each key we iterate through.

```terraform
locals {
  numbers         = [2, 4, 6]
     squared_numbers = {for number in local.numbers : number => number * number}
}
````

The above example produces the following object:

```console
$ terraform console
> local.squared_numbers
{
  "2" = 4
  "4" = 16
  "6" = 36
}
```

#### Declare a for loop that filters out elements

Optionally you can include an `if` clause in the `for` loop to filter out elements.

```terraform
data "aws_regions" "available" {}

locals {
  regions = [for name in data.aws_regions.available.names : name if != ""]
}
```

Want to learn more about For loops? [Check out the docs](https://www.terraform.io/language/expressions/for).

**Continue to [For each](../foreach)**
