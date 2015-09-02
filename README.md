# Terraform Style Guide

This is intended to be a guide of Terraform syntax and general best practices.
 
As Terraform utilises [HCL](https://github.com/hashicorp/hcl), you may wish to take a detailed look at its
[syntax guide](https://github.com/hashicorp/hcl/blob/master/README.md#syntax).

Inspired by [The Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) and
[The Puppet Style Guide](https://docs.puppetlabs.com/guides/style_guide.html).

## Table of Contents

* [Code Layout](#code-layout)
* [Modules](#modules)
* [Variables](#variables)
* [Outputs](#outputs)
* [Comments](#comments)

## Code Layout

Indentation should be 2 spaces (soft tabs). No hard tabs.

Attribute assignments (`=`) should be aligned for clarity.

```hcl
// bad
resource "aws_security_group" "main" {
    name = "${var.name}"
    description = "Security Group ${var.name}"
    vpc_id = "${var.vpc_id}"
    tags {
        Name = "${var.name}"
    }
}

// good
resource "aws_security_group" "main" {
  name        = "${var.name}"
  description = "Security Group ${var.name}"
  vpc_id      = "${var.vpc_id}"
  tags {
    Name = "${var.name}"
  }
}
```

## Modules

## Variables

Variables should be provided in a `variables.tf` file at the root of your project.

A description should be provided for each declared variable.

```hcl
// bad
variable "vpc_id" {}

// good
variable "vpc_id" {
  description = "The VPC this security group will go in"
}
```

## Outputs

Outputs should be provided in an `outputs.tf` file at the root of your project.

## Comments

Only comment what is necessary.

Single line comments: `#` or `//`.

Multi-line comments: `/*` followed by `*/`.
