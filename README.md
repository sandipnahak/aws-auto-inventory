<!--
  ** MANAGED BY AWS CODE HABITS
  ** DO NOT EDIT THIS FILE
  **
  ** 1) Make all changes to `doc/habits.yaml`
  ** 2) Run `make doc/build` to rebuild this file
  **
-->

![logo][logo]


# AWS Automated Inventory

Automates creation of detailed inventories from AWS resources.

### Problem
Projects usually have several resources and fetching all the information about these resources manually is a very time-consuming task.
This issue is intensified when the same project have multiple account and/or environments, e.g.: NonProd, QA and/or Prod.

### Solution
Provide a simple way to fetch the required information and generate a spreadsheet.
The information can be filtered, e.g. filter results by tag:x, vpc, subnets, etc.
Additionally, inventories can be generated related to many services, which are collected and organized per sheet in the spreadsheet.


## Table of Contents


- [Prerequisites](#prerequisites)

- [Installation](#installation)

- [Usage](#usage)


- [Testing](#testing)



## Prerequisites
  A list of things you need, or how to install them.

- [Python 3](https://www.python.org) - Python is a high-level, general-purpose programming language.


## Installation
Download the binary under [releases](https://github.com/aws-samples/aws-auto-inventory/releases).


## Usage
```
aws-auto-inventory --help
usage: aws-auto-inventory [-h] --name NAME
Automates creation of detailed inventories from AWS resources.
optional arguments:
  -h, --help            show this help message and exit
  --name NAME, -n NAME  inventory name
```


## Testing
AWS-Auto-Inventory uses [boto3](https://github.com/boto/boto3).
You can use any service that contains any list or describe method to fetch information about your resources.
### Parameters
You can use [boto3](https://github.com/boto/boto3) parameters to narrow down your search results.
#### Filter by tag:Name
```
sheets:
  - name: VPC
    service: ec2
    function: describe_vpcs
    result_key: Vpcs
    parameters:
      Filters:
        - Name: tag:Name
          Values:
            - my-vpc
```
### Filter by vpc-id
```
sheets:
  - name: Subnets
    service: ec2
    function: describe_subnets
    result_key: Subnets
    parameters:
      Filters:
        - Name: vpc-id
          Values:
            - vpc-xxx
```
### Find a particular RDS instance
```
sheets:
  - name: RDS
    service: rds
    function: describe_db_instances
    result_key: DBInstances
    parameters:
      DBInstanceIdentifier: the-name-of-my-rds-instance
```
### Find EC2 instances by a particular tag
```
sheets:
  - name: EC2
    service: ec2
    function: describe_instances
    result_key: Reservations
    parameters:
      Filters:
        - Name: tag:ApplicationName
          Values:
            - my-application
```
### Find a particular IAM Role
```
sheets:
  - name: IAM.Role
    service: iam
    function: get_role
    result_key: Role
    parameters:
      RoleName: my-role
```
  ### Development
```
# Linux/MacOS:
# clone the project and enter cloned directory
make init build
./dist/aws-auto-inventory --name <your-inventory-name>
```



- [AWS Code Habits][aws-code-habits] - A library with Make targets, Ansible playbooks, Jinja templates (and more) designed to boost common software development tasks and enhance governance.

## License
This project is licensed under the Apache License 2.0 License. See the [LICENSE](LICENSE) file.

## Copyright
Copyright Amazon, Inc. or its affiliates. All Rights Reserved.


[repo]: https://github.com/aws-samples/aws-auto-inventory
[logo]: doc/logo.png

[aws-code-habits]: https://github.com/awslabs/aws-code-habits

[habits]: https://github.com/awslabs/aws-code-habits
