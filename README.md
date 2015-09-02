# Terraform Style Guide

This is intended to be a guide of Terraform syntax and general best practices.
 
As Terraform utilises [HCL](https://github.com/hashicorp/hcl), you may wish to take a detailed look at its
[syntax guide](https://github.com/hashicorp/hcl/blob/master/README.md#syntax). 

## Table of Contents

* [Indentation](#indentation)
* [Modules](#modules)
* [Variables](#variables)
* [Outputs](#outputs)
* [Comments](#comments)

## Indentation

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

## Comments

Only comment what is necessary.

Single line comments: `#` or `//`.

Multi-line comments: `/*` followed by `*/`.
