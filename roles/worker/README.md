worker
=========
Role to setup the worker configuration in K8S_worker1 and K8S_worker2 (instance name) instance. It also automatically joins the master node and forms cluster.

Requirements
------------

`boto` `boto3` `botocore` packages are required.

Role is only tested on `ansible 2.10.3` version.

Role Variables
--------------
```
#update the src location if you put the automation file in different location. 
#EXAMPLE:  [/root/<dir>/worker/files/master_token.fact] 

copy_src_dir: /root/<dir>/worker/files/master_token.fact
```

Dependencies
------------
The master node role file you can find here 
* [master role](https://galaxy.ansible.com/rahulkumar0909/master "master role")

Also, if you need aws_ec2 role for launching perticular instance for master and worker role then you can find it here
* [aws_ec2 role](https://galaxy.ansible.com/rahulkumar0909/aws_ec2 "aws_ec2 role")

Joining worker node to master node is not compulsory you can also launch worker node only.


Example Playbook
----------------

```
- name: Worker K8S conf file configuration
  copy: 
      dest: /etc/systl.d/k8s.conf
      content: "{{ k8s_conf }}"
```

Used facts to auto join worker to Master
```
- name: Joining all worker nodes to Master node
  shell: "{{ ansible_local['master_token']['worker_token_cmd']['token_cmd'] }}"
  ignore_errors: True          
```


Author Information
------------------

### Connect me
* [Linkedin](https://linkedin.com/in/rahulkumar-choudhary-b662761a2 "Rahulkumar Choudhary")
* [Twitter](https://twitter.com/Rahulkumar29420 "Rahulkumar29420")
* [Medium](https://rahulchoudhary5768.medium.com/ "Rahulkumar Choudhary")
