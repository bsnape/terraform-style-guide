# Terraform Style Guide
This is intended to be a guide of Terraform syntax and general best practices. 
 
As Terraform utilises [HCL](https://github.com/hashicorp/hcl), you may wish to take a detailed look at its
[syntax guide](https://github.com/hashicorp/hcl/blob/master/README.md#syntax). Use the built-in 
[`terraform fmt` command](https://www.terraform.io/docs/commands/fmt.html) to format your Terraform 
in a manner consistent with this style guide.

Inspired by [The Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) and
[The Puppet Style Guide](https://docs.puppetlabs.com/guides/style_guide.html).

## Table of Contents
* [Code Layout](#code-layout)
* [File and Path Layout](#file-and-path-layout)
  * [Terraform Configuration](#terraform-configuration)
    * [Grouping Resources in Files](#grouping-resources-in-files)
  * [Module Paths](#module-paths)
    * [Private Modules](#private-modules)
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

## File and Path Layout
### Terraform Configuration
The primary (or only) Terraform configuration in a repo should be placed in the `/terraform` directory.

### Grouping Resources in Files
Files are used to group a series of resources (or data sources, providers, etc.) together. While different situations
call for different strategies in resource grouping, a good starting point is to place resource types with the same
prefix in a single file.  Becuase plural filenames (ie: `modules.tf`, `variables.tf`, `locals.tf`) are already widely
in inconsistent use, it is not advised to consider it significant.

If more than one resource type exists in a file that all share a given prefix, a distinction can be made by appending
an underscore to the filename. This retains expected compatiblility with shell filename completion and provides an easy
visual indicator.

Example file contents:
```hcl
resource "aws_alb" "uno" {
  ...
}

resource "aws_alb" "dos" {
  ...
}

resource "aws_alb_listener" "uno" {
  ...
}

resource "aws_alb_listener" "dos" {
  ...
}
```
The above filename should be called `aws_alb_.tf`. This ensures the filename reflects the contents, and remains
compatible with alphabetic sorting, grouping, and shell command completion

## Module Paths
The defacto standard location for modules which are exported is in the `/modules` path of the repo.

### Private Modules
For private modules (modules which are used exclusively by a configuration and are sourced using the direct path
name), place them immediately under configuration directory, ie: `/terraform/example_module`.

## Variables
Variables should be provided in a `variables.tf` file at the root of your project.

A description should be provided for each declared variable, unless a reasonable description adds no additional
information to the purpose of the variable (ie: the variable name is truly self documenting).

```hcl
// bad
variable "vpc_id" {}

// good
variable "vpc_id" {
  description = "The VPC this security group will go in"
}
```

## Outputs
Outputs should be provided in an `outputs.tf` file at the root of your project. Like variables, an output should
contain a description attribute unless it is truly self-documenting.

## Comments
Only comment what is necessary.

Single line comments: `#` or `//`.

Multi-line comments: `/*` followed by `*/`.
