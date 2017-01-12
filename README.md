# Code sample for provisioning EC2 instance with Flask webapp with Ansible

This repository contains Ansible playbook to deploy an EC2 instance and configure to run a simple flask web application.
The playbook can create a VPC, a subnet, a security group and a keypair, or existing infrastructure can be used.

## Pre-requisite

To run the playbook, ansible and boto need to be installed on local machine.
`pip install ansible boto`

Following environment variables need to be configured for AWS credentials.

`AWS_ACCESS_KEY_ID=AKIAICLGP*********`
`AWS_SECRET_ACCESS_KEY=rb8yX5I5s980sUA3LT**********`

## Usage instruction

With no existing infrastructure, following command will configure a simple VPC, subnet, a keypair, and launch an EC2 instance.

`ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook provision.yaml -u ubuntu`

If some of the infrastructure is already provisioned, these can be specified in `provision.yaml` as variables.
When existing private key is used, --private-key argument needs to be set.

`ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook provision.yaml -u ubuntu --private-key=PRIVATE_KEY_FILE`

## Verifying the web application
At the end of the playbook run, launched EC2 instance's Public IP will be showing.
```
PLAY RECAP *********************************************************************
54.199.240.116             : ok=7    changed=6    unreachable=0    failed=0
localhost                  : ok=12   changed=8    unreachable=0    failed=0
```

This IP address will be serving a very simple webserver running on flask which will return `Beautiful Webapp!`
```
$ curl 54.199.240.116
Beautiful Webapp!
```