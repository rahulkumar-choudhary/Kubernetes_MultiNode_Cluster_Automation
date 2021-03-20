master
=========
Role to setup the master configuration in aws K8S_master (instance name) instance.

Requirements
------------

`boto` `boto3` `botocore` packages are required.

Role is only tested on `ansible 2.10.3` version.

Role Variables
--------------
```
#update the dest location of worker role file if you put the role file in different location. 
#EXAMPLE: [/root/<dir>/worker/files] 

fetch_dest_dir: /root/<dir>/worker/files/

#remove mater_token.fact file if it is already present or else fetch module wont work.
```

Dependencies
------------
The worker node role file you can find here 
* [worker role](https://github.com/Rahulkumar0909/Kubernetes_MultiNode_Cluster_Automation/tree/master/roles/worker "worker role")

Also, if you need aws_ec2 role for launching perticular instance for master and worker role then you can find it here
* [aws_ec2 role](https://galaxy.ansible.com/rahulkumar0909/aws_ec2 "aws_ec2 role")

Joining worker node is not compulsory you can also launch master node only.


Example Playbook
----------------

```
- name: Kubeadm init 
  shell: "{{ kube_init }}"
  ignore_errors: True
```

Used facts to auto join worker to Master
```
- name: Fetch fact file from master to local
  fetch:
      dest: "{{ fetch_dest_dir }}"
      src: /etc/ansible/facts.d/master_token.fact
      flat: yes 
  ignore_errors: True          
```


Author Information
------------------

### Connect me
* [Linkedin](https://linkedin.com/in/rahulkumar-choudhary-b662761a2 "Rahulkumar Choudhary")
* [Twitter](https://twitter.com/Rahulkumar29420 "Rahulkumar29420")
* [Medium](https://rahulchoudhary5768.medium.com/ "Rahulkumar Choudhary")

