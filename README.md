
### Installing Contrail on an existing Openshift cluster

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

5. Please append contrail parameters to your openshift inventory.

   ```

   openshift_use_openshift_sdn=false
   os_sdn_network_plugin_name='cni'
   openshift_use_contrail=true
   contrail_version=5.0
   contrail_container_tag=5.0.1-0.214
   contrail_registry_insecure=true
   contrail_registry=hub.juniper.net/contrail
   # Username /Password for private Docker registry
   #contrail_registry_username=test
   #contrail_registry_password=test
   #vrouter_gateway=10.10.10.1

   #**Add this contrail vars list**
   [contrail_masters]
   10.10.10.10 openshift_hostname=ip-10-10-10-10.us-west-1.compute.internal
 
 
  ```
  
6. Run the deploy_contrail.yml file

   ```
   
   cd <path-to-your-openshift-ansible>/playbooks
   ansible-playbook -i inventory/ose-install deploy_contrail.yml
    
    ```


This playbook will install Contrail.
 
 


