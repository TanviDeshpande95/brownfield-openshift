
# Installing Contrail on an existing Openshift cluster

# Overview:

Ansible playbooks to install contrail in a Brownfield Openshift deployment. The playbooks let users install Contrail on an existing Openshift cluster.

# Prerequisites:
  This document assumes you have Openshift 3.9 installed on your system.

# Steps to execute:

1. Pull the brownfield-openshift repository on your system
   ```
   sudo git clone https://github.com/TanviDeshpande95/brownfield-openshift.git
   ```

2. Run this playbook to copy required files into your openshift-ansible directory.
   ```
   cd brownfield-openshift/playbooks
   ```
   ```
   ansible-playbook copy_master.yml -e dst_directory=<path to your openshift-ansible
   ```

 ```
 [root@ip-10-10-10-10 playbooks]# ansible-playbook copy_master.yml -e dst_directory=/root/openshift-ansible-new
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not
  match 'all'
 [WARNING]: Ignoring invalid attribute: dest
 PLAY [127.0.0.1]
 *****************************************************************************************************************
 TASK [Gathering Facts]
 ***********************************************************************************************************
 ok: [127.0.0.1]
 TASK [copy modified os_contrail_master.yaml into your openshift-ansible-deployer roles]
 ******************************************
 changed: [127.0.0.1]
 PLAY RECAP
 *****************************************************************************************************************
 ******
 127.0.0.1                  : ok=2    changed=1    unreachable=0    failed=0
 ```
3. Copy deploy_contrail.yml to your openshift-ansible playbooks folder
   ```
   cp deploy_contrail.yml <path to your openshift-ansible>/playbooks
   ```

4. Append Contrail SDN roles and config to your openshift-ansible

   Refer to [custom-openshift](https://github.com/Juniper/custom-openshift) for appending Contrail SDN roles to
 your openshift-ansible deployer.

  
5. Run the deploy_contrail.yml file to install contrail

   ```
    cd <path-to-your-openshift-ansible>
    ansible-playbook -i inventory/ose-install playbooks/deploy_contrail.yml
    ```
 


