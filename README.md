# Ansible Collection - rahulgitx.kubernetes

Documentation for the collection.


###  Configuration of a 3-node( 1 master and 2 worker) kubernetes cluster on AWS instances with the help of ansible roles.

For **quick configuration** just download all of these files in your local folder and keep in mind the following steps:
* Add your AWS user key and ID by running ```export AWS_ACCESS_KEY_ID='AKIA**************'``` and ```export AWS_SECRET_ACCESS_KEY='6+SCCNzQ68OqfK**********************' ``` command on the current folder.
* Add the keys in _your_path_/role/launching_instances/vars/main.yml file as well.
* Add the name of the key that you will be using in the instances in the same file as well. (Note: do not use any .pem or .ppk extension here)
* Make sure you have the .pem file of the key in your same folder where you'll the main.yml file.
* Add the name of your private key in the ansconf line 137.
* Run ```ansible-playbook main.yml```
* For more details follow [this article](www.medium "how to configure")
* The instances are made with specific tags to interact with so while making the main.yml file keep in mind to not making deviation from the following logic:
```
 - hosts: localhost
  roles:
          - role: launching_instances
            ignore_errors: yes

- hosts: tag_ansible_mn
  roles:
          - role: docker
            ignore_errors: yes

- hosts: tag_k8s_master
  roles:
          - role: k8smaster
            ignore_errors: yes

- hosts: tag_k8s_node
  roles:
          - role: k8sworker
            ignore_errors: yes
```
_Note: By default this role will launch three amazon linux free tier t2.micro instances in Mumbai region. Make changes in the role/launching_instances/vars/main.yml folder to customize according to you._

