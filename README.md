# Ansible role: AWS VPC IGW

This role handles the creation of Internet Gateways for a VPC in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable              | Description                  |
|-----------------------|------------------------------|
| `aws_vpc_igw_profile` | Boto profile name to be used |


## Example definition

#### Required parameter only

```yml
aws_vpc_igws:
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
