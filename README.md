vpc terraform module
===========

A terraform module to provide a VPC in AWS.


Module Input Variables
----------------------

- `name` - vpc name
- `cidr` - vpc cidr
- `enable_dns_hostnames` - should be true if you want to use private DNS within the VPC
- `enable_dns_support` - should be true if you want to use private DNS within the VPC
- `enable_nat_gateway` - should be true if you want to provision NAT Gateways for each of your private networks
- `map_public_ip_on_launch` - should be false if you do not want to auto-assign public IP on launch
- `private_propagating_vgws` - list of VGWs the private route table should propagate
- `public_propagating_vgws` - list of VGWs the public route table should propagate
- `tags` - dictionary of tags that will be added to resources created by the module

This module optionally creates NAT Gateways in each public subnet and sets them
as the default gateways for the corresponding private subnets.

Usage
-----

```hcl
module "vpc" {
  source = "github.com/terraform-community-modules/tf_aws_vpc"

  name = "my-vpc"
  cidr = "10.0.0.0/16"
  enable_nat_gateway = "true"

  tags {
    "Terraform" = "true"
    "Environment" = "${var.environment}"
  }
}
```

Outputs
=======

 - `vpc_id` - does what it says on the tin
 - `private_subnets` - list of private subnet ids
 - `public_subnets` - list of public subnet ids
 - `database_subnets` - list of database subnets ids
 - `database_subnet_group` - db subnet group name
 - `public_route_table_ids` - list of public route table ids
 - `private_route_table_ids` - list of private route table ids
 - `default_security_group_id` - VPC default security group id string
 - `nat_eips` - list of Elastic IP ids (if any are provisioned)
 - `nat_eips_public_ips` - list of NAT gateways' public Elastic IP's (if any are provisioned)
 - `natgw_ids` - list of NAT gateway ids
 - `igw_id` - Internet Gateway id string

**NOTE**: previous versions of this module returned a single string as a route
table ID, while this version returns a list.

Authors
=======

Originally created and maintained by [Casey Ransom](https://github.com/cransom)
Hijacked by [Paul Hinze](https://github.com/phinze)

License
=======

Apache 2 Licensed. See LICENSE for full details.
