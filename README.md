k8s-hetzner-cluster
=========

A ansible role to create a kubernetes cluster in hetzner cloud provider

Requirements
------------

Basically you need minimum of two  Ubuntu Servers(**CX11**) with version **20.04** and a private network to connect the cluster internally.

The servers should be grouped, for example
```
  [k8s-masters]
  k8s-master ansible_host=125.111.126.68 ansible_user=k8s

  [k8s-workers]
  k8s-node1 ansible_host=135.181.107.190 ansible_user=k8s
  k8s-node2 ansible_host=133.121.127.110 ansible_user=k8s
```

###### IMPORTANT
When you create the servers, you need to select the user data option and paste the [yaml content](https://github.com/eugeni9872/ansible-k8s-cluster/blob/main/k8s-cluster/files/hcloud_user.yml) to create the an user with password-

> You can change the hashed password with following [this](https://cloudinit.readthedocs.io/en/latest/topics/examples.html) guide

Also you need a token with read & write permissions that you can create following Project Name -> Security -> API Tokens


Role Variables
--------------
You need to provide the following vars 
  1. hcloud_token: The hetzner api token
  2. hcloud_private_network: The private network name or id
  3. float_ip_addr: The float ip allow you to access with a public IP to your ingress. If is not defined, loadbalancer config will be used by default.


Example Playbook
----------------
      hosts: all
      become: true
      roles:
        - {role: k8s-cluster, hcloud_token:'Hetnzer token', hcloud_private_network:'private network name/ID', etc... }


License
-------

BSD

Eugeni Bejan
------------------