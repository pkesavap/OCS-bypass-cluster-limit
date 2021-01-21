OCS-bypass-cluster-limit
=========

This Ansible role can be used when your cluster capacity passes the ocs threshold of 85% and you essentially cannot delete your pvc or pv, because the cluster will go full 'read-only' mode, essentially not allowing to delete pvc or pv.

Requirements
------------
You need to:-

[1] Install ceph toolbox into your openshift cluster.

[2] oc login to your cluster, wherever this ansible roles is going to be executed

Role Variables
--------------
This Ansible Role requires the following variables as input:


| Name                     | Required? | Choices| Default value         | Comments                          |
|--------------------------|----|---|-----------------------|-----------------------------------|
| ceph_toolbox_pod_name | Yes |  | UNDEF   | Ceph toolboc pod name |
| pv_list | Yes|  | UNDEF | List of pv to be deleted. |
| pvc_list | Yes | | UNDEF | TList of PV you want to erase.|


[1] Ceph toolboc pod name

[2] List of pvc you want to delete

[3] List of PV you want to erase

Dependencies
------------

No other Dependencies required as of now
Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
---
- hosts: cluster_node
  connection: local
  remote_user: root
  gather_facts: no
  tasks:
    - block:
      - name: Reconfigure Ceph Cluster
        include_role:
          name: OCS-bypass-cluster-limit
_____________
```
```

vars.yml:-
---
cluster_node:
  hosts:
   localhost.localdomain
  vars:
   ceph_toolbox_pod_name: "tooldbox_pod_name"
   pv_list:
     - { "pv1" }
     - { "pv2" }
     - { "pv3" }
   pvc_list:
     - { "pvc1" }
     - { "pvc2" }
     - { "pvc3" }
```

License
-------

BSD

Additional Information
------------------
This role is still going through a series of developmental process and is untested, unless otherwise stated.



Author Information
------------------
Prajith Kesava Prasad (@pkesavap)

