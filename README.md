# Ansible role: AWS VPC IGW

This role is able to create any number of Internet Gateways, each attached to a VPC in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                     | Description                  |
|------------------------------|------------------------------|
| `aws_vpc_igw_profile`        | Boto profile name to be used |
| `aws_vpc_igw_default_region` | Default region to use        |


## Example definition

IGW's can be created per VPC either by supplying a VPC `name` or a VPC `filter`.

#### Required parameter only

```yml
aws_vpc_igws:
  # Create IGW for a VPC by VPC name
  - vpc_name: devops-test-vpc
  # Create IGW for a VPC by VPC filter
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
```

#### All available parameter
```yml
aws_vpc_igws:
  # Create IGW for a VPC by VPC name
  - vpc_name: devops-test-vpc
    region: eu-central-1
    tags:
      - key: Name
        val: devops-test-igw
      - key: env
        val: playground
      - key: department
        val: devops
  # Create IGW for a VPC by VPC filter
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    region: eu-central-1
    tags:
      - key: Name
        val: devops-test-igw
      - key: env
        val: playground
      - key: department
        val: devops
```
