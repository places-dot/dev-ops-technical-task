# DevOps Engineer Technical Test Task

This technical task is designed to assess the practical skills of candidates applying for the DevOps Engineer position.

## Requirements

- AWS
- HashiCorp Terraform
- Ansible
- Kubernetes
- Docker
- (Optional) Ruby and Ruby on Rails

## Overview

To complete this technical task, you need to build a cloud deployment infrastructure to deploy a Ruby on Rails application to AWS. Please demonstrate your practical skills using the standard toolkit technologies described in the following steps and adhere to best practices. Some points in the task have optional elements; implementing all or some of these will be considered a plus.

## Task

Create AWS-based cloud infrastructure to run a Ruby on Rails application.

### 1. Terraform AWS Provisioning

Use the official Terraform AWS modules:
https://registry.terraform.io/providers/hashicorp/aws/latest/docs

1. Provision an AWS VPC with private and public networks.
2. Provision AWS infrastructure to run Minikube on an AWS EC2 instance in the private network.
3. Provision an AWS RDS multi-AZ instance in the private network.
4. Provision an AWS ELB routing from the public network to the private network.
5. (Optional, is a plus) Provision an AWS ACM certificate and attach it to the ELB.
6. Provision AWS ECR.
7. (Optional, is a plus) Provision any required AWS IAM roles and policies.
8. (Optional, is a plus) Automatically pass values required for Ansible and/or Kubernetes manifests.

### 2. Ansible Minikube Deployment

1. Create an Ansible playbook to deploy a Minikube cluster to AWS EC2.
2. (Optional, is a plus) The playbook should gather data and facts from Terraform outputs.

### 3. Container Images

Create multi-stage Dockerfiles for container images to run the application and worker.
1. Create a base Ruby image using the latest Alpine Linux. Build the Ruby interpreter from source code, use YJIT, and pass the required compiler flags.
2. Based on the built image, create a second target with the application.
3. (Optional, is a plus) If the worker application requires additional features, depending on your solution, create a third target.
4. Push images to the provisioned AWS ECR.

### 4. Kubernetes Manifests

Create a set of Kubernetes manifests to deploy the application and worker to the cluster.
(Optional, is a plus) Use Terraform module: (https://registry.terraform.io/providers/hashicorp/kubernetes/latest)

1. Create an application deployment that runs the Rails application.
2. Create a worker deployment that runs the GoodJob background processor.
3. Create the necessary services and ingresses to expose the application from port 3000 to ports 80/443 and interconnect with the ELB.

### 5. (Optional, is a plus) Application

To use an already built application, please request the URL to the repository.

Requirements:
- Ruby ~> 3.2
- Ruby on Rails ~> 7.1

Use the following gems:
- rails_performance (https://github.com/igorkasyanchuk/rails_performance)
- good_job (https://github.com/bensheldon/good_job)

1. Accepts requests to the following routes as JSON documents or HTML forms:
   - GET /log_request?<any_param>=“param value”
   - POST /log_request?<any_param>=“param value”
   - PUT /log_request?<any_param>=“param value”
   - PATCH /log_request?<any_param>=“param value”
2. Returns the following JSON response document:

```json
{
  "body": <body object>,
  "params": <request params object>,
  "headers": <headers object>
}
```
3. (Optional, is a plus) Stores requested data in the PostgreSQL database as JSON.
4. Shows request statistics using `rails_performance`.


### 6. Push solution to the github or any other git repository.
