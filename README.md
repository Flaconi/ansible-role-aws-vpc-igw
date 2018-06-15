# Ansible role: AWS VPC IGW

This role is able to create any number of Internet Gateways, each attached to a VPC in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-igw)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-igw.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-igw/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25920.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-igw/)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                            | Description                  |
|-------------------------------------|------------------------------|
| `aws_vpc_igw_profile`               | Boto profile name to be used |
| `aws_vpc_igw_default_region`        | Default region to use        |
| `aws_vpc_igw_vpc_filter_additional` | Additional `key` `val` filter to add to `vpc_filter` and `vpc_name` by default. |


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
# Ensure VPC filter (name or filter) includes that the VPC is created already
# (not pending nor deleted)
aws_vpc_igw_vpc_filter_additional:
  - key: state
    val: created

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


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
