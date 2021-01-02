# Ansible : INstall kubernetes cluster on multipass VM's

[![CI](https://github.com/geerlingguy/ansible-role-kubernetes/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-kubernetes/actions?query=workflow%3ACI)


## Ansible Playbook Variables

Available variables are listed below, along with default values:
* Host_Vars & Group_Vars:
    ansible_host: ` `
    kubernetes_role: ` see Readme for kuberntes role`


## Dependencies

### Roles

* Use roles in order to make an automated playbook to install your dependencies and requirements and setup your kubenretes cluster with one master and *n* nodes.

## Example Playbooks

Playbook:

```yaml
---
- name: Master and slave requirements
  hosts: masters, slave
  vars:
    kubernetes_allow_pods_on_master: true
  vars_files: 
    - roles/docker/vars/default.yml
    - group_vars/masters.yml
    - roles/user-system/vars/default.yml
    #if you want to use rkt runtime
    - roles/elyess.rkt/vars/default.yml
    # test reachability of your cluster
  pre_tasks:
    - name: Is alive
      ping:
    
  roles:
    - { role: upgrades, tags: ["os_upgrade"]}
    - { role: user-system, tags: ["ubuntu"]}
    
    - { role: dependencies, tags: ["python", "transport_layer"] }
    - { role: elyesbenamor.docker,become: true, become_methods: sudo, tags: ["geer-docker"]}
    - { role: elyesbenamor.kubernetes, become: true, become_methods: sudo, tags: [geer-kuber]}

    # if you want to use rkt role instead of docker one 
    - - { role: elyesbenamor.ansible_role_rkt, tags: [rkt]}


```

Then, log into the master, and run `kubectl get nodes` as ubuntu non root user, and you should see the nodes are created .

## License

MIT / BSD

