# DevOps Engineer Technical Test Task

Current technical task is task required to check practical skills of candidate to the DevOps engineer position.

## Requirements

- AWS
- HasiCorp Terraform
- Ansible
- Kubernetes
- Docker
- (Optional) Ruby and Ruby on Rails

## Overview

To complete current technical task you need to build cloud deployment infrastracture to deploy Ruby on Rails applicarion to the AWS.
Please, demonstrate your practical skills using standard toolkit technologies described at the next steps and best prcatices.
Some task points, have a optional points, so implementing al of them or some of them will be a plus.

## Task

Create AWS based cloud infrastructure to run Ruby on Rails application.

### 1. Terraform AWS provisioning

Using terraform official modules
https://registry.terraform.io/providers/hashicorp/aws/latest/docs

1. Provision AWS VPC with private and public networks.
2. Provision AWS infrastructure to run minikube on the AWS EC2 instance at the private network.
3. Provision AWS RDS multi-AZ instance at the private network.
4. Provision AWS ELB passing public network to the private network.
5. (Optional, is a plus) Provision AWS ACM certificate and attach it on top of the ELB.
6. Provision AWS ECR.
7. (Optional, is a plus) Provision any required AWS IAM roles and policies.
8. (Optional, is a plus) Passes automatically values, required for ansible and/or kubernetes manifests

### 2. Ansible minikube deployment

1. Create Ansible playbook to deploy minikube cluster to the AWS EC2.
2. (Optional, is a plus)Playbook should gather data and facts from Terraform outputs.
3. 

### 3. Container images

Create multi-stage Dockerfiles for container images to run application and worker.
1. Create base ruby image using latest Alpina linux. Build ruby interpretter from source code, use YJIT and pass required compiler flags.
2. Basing on the built image create second target with application. 
3. (Optional, is a plus) If worker application will require some additional features, depending on your solution - create third target. 
4. Push images to the provisioned AWS ECR

### 4. Kubernetes manifests

Create set of Kubernetes manifests to deploy application and worker to the cluster.

1. Create application deployment, running rails application
2. Create worker deployment, running good_job background processor
3. Create required services and ingresses to pass out application from port 3000 to 80/443 and interconnect with ELB.

### 5. (Optional, is a plus) Application
In case to use already built appliation, please ask about url to the repository.

Requirements:
 - Ruby ~> 3.2
 - Ruby on Rails ~> 7.1

Use next gems:
- rails_performance(https://github.com/igorkasyanchuk/rails_performance)
- good_job(https://github.com/bensheldon/good_job)

1. It receives requst to the next routes as JSON document or HTML form 
- GET /log_request?<any_param>="param value"
- POST /log_request?<any_param>="param value"
- PUT /log_request?<any_param>="params value"
- PATCH /log_request?<any_param>="params value"
2. Returns next response as JSON with document:

```
{
  "body": <body object>,
  "params": <request params object>,
  "headers": <headers object>
}
```
3. (Optional, is a plus)Stores requested data to the PostgreSQL database as a json.
4. Shows request statistics using rails_performance
