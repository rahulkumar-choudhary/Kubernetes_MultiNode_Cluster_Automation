# Automation: Kubernetes Multi-Node Cluster On  AWS Cloud Using Ansible


<p align="center">
  <img src="https://miro.medium.com/max/875/1*borj4CAzNB3a8kixeqzqwQ.gif?raw=true" width="525" height="400" />
</p>



## System Requirements
These roles have only been tested with:
* RedHat Linux `8`,`7`
* Ansible version:
  * `2.10.3`

In addition, the roles specifically target the `RedHat OS` family, including `CentOS` and `Amazon Linux`, and may not function for other host OS's.


## Prerequisite
Require Ansible version 2.10.3 installed.

You can create virtual environment and begin.

refrence link for virtualenv setup :
[virtual environment setup](https://rahulchoudhary5768.medium.com/install-virtualenv-and-virtualenvwrapper-for-python3-6676267c07ee "Installing virtualenv and virtualenvwrapper for Python")

In that virtualenv run the following command:
```bash
pip3  install 'ansible==2.10.3' 
```


## Getting Started

This repository contains Ansible roles for Automating the Kubernetes Multi-Node Cluster on AWS cloud. Even all two worker nodes automatically join the master node.
<!-- Each role contains a README describing its usage.-->
By default as in aws_ec2 role only two worker node are launched but you can launch more than two worker node by modifying the code as per ypur need.

## Steps to do
* Put the AWS EC2  `key-pair` file in     `/Kubernetes_MultiNode_Cluster_Automation/aws_key_pem` directory.
*   Update the value of the name of your [name].pem file in two files:
  *  `run_script_one` file:
  ```bash
  "chmod 400 ./aws_key_pem/[name].pem"
  ```

  *   `ansible.cfg` file:
  ```bash
  [defaults]
  private_key_file= ./aws_key_pem/[name].pem
  ```
* In aws_ec2 role in vars folder update the details of the AWS.

 Path: `/Kubernetes_MultiNode_Cluster_Automation/roles/aws_ec2/vars/main.yml`

 Here you need to update the aws `key-pair` name, `subnet_id` , `vpc_id` , `access_key` and `secret_key` details.

 ```yaml
 K8S_key_name: "aws_key"

 ->NOTE: "aws_key" means only the name of key-pair of aws
 ->EXAMPLE:  aws_key.pem so, only use aws_key

 subnet_id: "subnet-ID"
 vpc_id: "vpc-ID"
 access_key: "XXXXXXXXXXXXXXXXXX"
 secret_key: "XXXXXXXXXXXXXXXXXX"
  ```

* Make `run_script_one` file executable:
```bash
chmod +x run_script_one
```
---
> NOTE: This script assumes Ansible is being executed where the environment variables needed for Boto have already been set.
---
* ##### Run following commands manually in command line terminal to set environment variables needed for boto.
```bash
export AWS_ACCESS_KEY_ID='XXXXXXXXXXXXXXXXXX'
export AWS_SECRET_ACCESS_KEY='XXXXXXXXXXXXXXXXXX'
export AWS_REGION='ap-south-1'
```
---
>NOTE: Make sure the [name].pem file is present in the ./aws_key_pem file.
---


## For changes
Update some path name in master and worker roles if you have clone the repo in different directory.

* In `worker role` :
Update the dest location if you put the automation file in different location.

EXAMPLE: `/root/<dir>/Kubernetes_MultiNode_Cluster_Automation/roles/worker/files`

* In `master node`:

Update the src location if you put the automation file in different location.

EXAMPLE:  `/root/<dir>/Kubernetes_MultiNode_Cluster_Automation/roles/worker/files/master_token.fact`

## Here user can use two approach 
* `Script` 
* `Manual` 

## Start

#### Run the script:
This will run all the playbook automatically so, no need to run `ansible-playbook` command.

Run command in terminal
```bash
./run_script_one
```

## OR
#### You can run playbook in sequential manner:

```bash
ansible-playbook  system_requirment.yml
```
> system_requirment.yml file will install some prerequisite software and python libraries on hoste OS.

```bash
ansible-playbook  ec2_provision.yml
```
>ec2_provision.yml file will run aws_ec2 role and it will provision the ec2 instances in AWS.

```bash
ansible-playbook  K8S_Cluster_setup.yml
```

>K8S_Cluster_setup.yml file will run first master role which will setup the Kubernetes Master node in AWS master instance and  then will run worker role which will setup worker node in AWS worker1 and worker2 instances and will automatically join all the worker nodes to master node.

### Connect me
[Here!](https://bio.link/linkrahulkumar "Rahulkumar Choudhary")
