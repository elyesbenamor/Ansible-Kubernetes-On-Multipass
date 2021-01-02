# Ansible Role: rkt

[![CI](https://github.com/geerlingguy/ansible-role-kubernetes/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-kubernetes/actions?query=workflow%3ACI)

An Ansible Role that installs [Rkt](https://coreos.com/rkt/docs/latest/) on Linux.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    Ansible_User:
      ansible_ssh_user: ubuntu


Apt repository options for Rkt installation.

    Rkt_Package:
      - https://github.com/coreos/rkt/releases/download/v{{ rkt_version }}/rkt-v{{ rkt_version }}.tar.gz
   dest=/tmp/rkt.zip

## Useful links

Use try [rkt with kubernetes](https://coreos.com/rkt/docs/latest/using-rkt-with-kubernetes.html) to see how to integrate the rkt runtime on your cluster.

## Dependencies

None.

## Example Playbooks

Playbook:

```yaml
- hosts: all


  roles:
    - elyesbenamor.ansible_role_rkt
```

Then, log into the master, and run `rkt version` as ubuntu non root user, and you should see the version of your runtime rkt.

## License

MIT / BSD

