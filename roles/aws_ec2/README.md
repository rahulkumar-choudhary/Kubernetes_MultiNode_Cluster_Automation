aws_ec2
=========

Description
-----------
Launch security group and provision three ec2-instance (t2.micro). All the instances are launched parallelly i.e 𝐔𝐬𝐞𝐝 𝐀𝐬𝐲𝐧𝐜𝐡𝐫𝐨𝐧𝐨𝐮𝐬 𝐚𝐩𝐩𝐫𝐨𝐚𝐜𝐡, 𝐨𝐩𝐭𝐢𝐦𝐢𝐳𝐞𝐝 𝐟𝐨𝐫 𝐞𝐟𝐟𝐞𝐜𝐭𝐢𝐯𝐞 𝐚𝐮𝐭𝐨𝐦𝐚𝐭𝐢𝐨𝐧.

Requirements
------------

`boto` `boto3` `botocore` packages are required.

Role is only tested on `ansible 2.10.3` version.

Role Variables
--------------

Variables required in aws_ec2  role :
* default VPC-id
*Subnet-id
*region
*Access Key
*Secret Key

```
---
# vars file for aws_ec2
K8S_key_name: "aws_key"
subnet_id: "subnet-ID"
region: "ap-south-1"
vpc_id: "vpc-ID"
sg_id: "{{ security_group_k8s['group_id'] }}"
access_key: "XXXXXXXXXXXXXXXXXX"
secret_key: "XXXXXXXXXXXXXXXXXX"
```


Example Playbook
----------------
master node
```
- name: Launcing Master instances.
  ec2_instance:
    region: "{{ region }}"
    aws_access_key: "{{ access_key }}"
    aws_secret_key: "{{ secret_key }}"
    name: "K8S_Master"
    key_name: "{{ K8S_key_name }}"
    instance_type: "{{ inst_type }}"
    image_id: "{{ img_id }}"
    security_group: "{{ sg_id }}"
    vpc_subnet_id: "{{ subnet_id }}"
    network:
        assign_public_ip: true
    state: present
    tags:
        K8S : master
        Kube : cluster
    wait: yes
  async: 180
  poll: 0
```


Author Information
------------------
### Connect me
* [Linkedin](https://linkedin.com/in/rahulkumar-choudhary-b662761a2 "Rahulkumar Choudhary")
* [Twitter](https://twitter.com/Rahulkumar29420 "Rahulkumar29420")
* [Medium](https://rahulchoudhary5768.medium.com/ "Rahulkumar Choudhary")
