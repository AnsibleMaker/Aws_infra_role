# Infrastructure Role: README

This Ansible role `infra` is designed to automate the creation of infrastructure on AWS, including VPCs, subnets, internet gateways, route tables, security groups, and EC2 instances.

## Directory Structure

```
infra
├── README.md                # Documentation for the role
├── defaults
│   └── main.yml             # Default variables for the role
├── files                    # Static files used by the role (empty)
├── handlers
│   └── route_table_create.yml  # Handlers for route table creation tasks
├── meta
│   └── main.yml             # Metadata about the role
├── tasks
│   ├── ec2.yml              # Task for creating EC2 instances
│   ├── igw.yml              # Task for creating Internet Gateway
│   ├── main.yml             # Main task file for orchestrating tasks
│   ├── security.yml         # Task for creating Security Groups
│   ├── subnets.yml          # Task for creating Subnets
│   └── vpc.yml              # Task for creating VPCs
├── templates                # Jinja2 templates (empty)
├── tests
│   ├── inventory            # Inventory file for testing
│   └── test.yml             # Test playbook for verifying the role
└── vars
    └── main.yml             # Variable definitions used in the role
```

## Features
- Create a VPC with specified CIDR.
- Provision public and private subnets.
- Set up an Internet Gateway (IGW).
- Create and associate route tables.
- Configure Security Groups for public and private access.
- Deploy EC2 instances in the created VPC.

## Requirements
- Ansible 2.9 or later
- Python modules: `boto3` and `botocore`
- AWS credentials configured (via environment variables, credentials file, or Ansible vault)

## Role Variables
The role uses variables defined in `vars/main.yml` and `defaults/main.yml`. Key variables include:

| Variable           | Description                         | Example                      |
|--------------------|-------------------------------------|------------------------------|
| `cidr`            | CIDR block for the VPC             | `10.0.0.0/16`               |
| `subnet.public`   | CIDR block for public subnet        | `10.0.1.0/24`               |
| `subnet.private`  | CIDR block for private subnet       | `10.0.2.0/24`               |
| `loc`             | AWS region                         | `us-east-1`                 |

## Usage

### 1. Include the Role in Your Playbook
Create a playbook that includes this role:

```yaml
- name: Provision AWS Infrastructure
  hosts: localhost
  roles:
    - infra
```

### 2. Run the Playbook
Execute the playbook:

```bash
ansible-playbook -i inventory playbook.yml
```

## Testing
The role includes a test playbook (`tests/test.yml`) and inventory file (`tests/inventory`). Run the test using:

```bash
ansible-playbook -i tests/inventory tests/test.yml
```

## Notes
- Ensure AWS credentials are configured correctly.
- Use the `debug` module to inspect variables if tasks fail.
- Follow AWS best practices for CIDR block allocation and security group rules.

## Contributing
Feel free to submit issues or pull requests to enhance the functionality of this role.

## License
This role is licensed under the MIT License.

