# Ansible Role: Docker

[![CI](https://github.com/geerlingguy/ansible-role-docker/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-docker/actions?query=workflow%3ACI)

An Ansible Role that installs [Docker](https://www.docker.com) on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    docker_package_state: present

You can control whether the package is installed, uninstalled, or at the latest version by setting `docker_package_state` to `present`, `absent`, or `latest`, respectively. Note that the Docker daemon will be automatically restarted if the Docker package is updated. This is a side effect of flushing all handlers (running any of the handlers that have been notified by this and any other role up to this point in the play).

    docker_service_state: started
    docker_service_enabled: true
    docker_restart_handler_state: restarted

Variables to control the state of the `docker` service, and whether it should start on boot. If you're installing Docker inside a Docker container without systemd or sysvinit, you should set these to `stopped` and set the enabled variable to `no`.

    docker_install_compose: true
    docker_compose_version: "1.26.0"
    docker_compose_path: /usr/local/bin/docker-compose

Docker Compose installation options.

    docker_apt_release_channel: stable
    docker_apt_arch: amd64
    docker_apt_repository: "deb https://download.docker.com/linux/ubuntu bionic stable"
    docker_apt_ignore_key_error: True
    docker_apt_gpg_key: https://download.docker.com/linux/{{ ansible_distribution | lower }}/gpg

(Used only for Debian/Ubuntu.) You can switch the channel to `nightly` if you want to use the Nightly release.

You can change `docker_apt_gpg_key` to a different url if you are behind a firewall or provide a trustworthy mirror.
Usually in combination with changing `docker_apt_repository` as well.

    docker_yum_repo_url: https://download.docker.com/linux/centos/docker-{{ docker_edition }}.repo
    docker_yum_repo_enable_nightly: '0'
    docker_yum_repo_enable_test: '0'
    docker_yum_gpg_key: https://download.docker.com/linux/centos/gpg

A list of system users to be added to the `docker` group (so they can use Docker on the server).

## Use with Ansible (and `docker` Python library)

Many users of this role wish to also use Ansible to then _build_ Docker images and manage Docker containers on the server where Docker is installed. In this case, you can easily add in the `docker` Python library using the `geerlingguy.pip` role:

```yaml
- hosts: all

  vars:
    pip_install_packages:
      - name: docker

  roles:
    # use pip galaxy module role
    - elyesbenamor.docker
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - elyesbenamor.docker
```

## License

MIT / BSD

