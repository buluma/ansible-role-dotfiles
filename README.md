# Ansible role [dotfiles](https://galaxy.ansible.com/ui/standalone/roles/buluma/dotfiles/documentation)

Dotfile installation for UNIX/Linux.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-dotfiles/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-dotfiles/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-dotfiles.svg)](https://github.com/buluma/ansible-role-dotfiles/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-dotfiles.svg)](https://github.com/buluma/ansible-role-dotfiles/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-dotfiles.svg)](https://github.com/buluma/ansible-role-dotfiles/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/dotfiles)](https://galaxy.ansible.com/ui/standalone/roles/buluma/dotfiles/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-dotfiles/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true

  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=true cache_valid_time=600
      when: ansible_os_family == 'Debian'

  roles:
    - role: buluma.git
    - role: buluma.dotfiles
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-dotfiles/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: false
  become: true

  tasks:
    - name: Update Package Cache (apt/Ubuntu)
      tags: always
      apt:
        update_cache: yes
      changed_when: false
      when: ansible_distribution == "Ubuntu"

    - name: Update Package Cache (dnf/CentOS)
      tags: always
      dnf:
        update_cache: yes
      changed_when: false
      when: ansible_distribution == "CentOS"

    - name: Update Package Cache (yum/Amazon)
      tags: always
      yum:
        update_cache: yes
      changed_when: false
      when: ansible_distribution == "Amazon"

  roles:
    - role: buluma.bootstrap
    # - role: buluma.git
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-dotfiles/blob/master/defaults/main.yml):

```yaml
---
dotfiles_repo: "https://github.com/buluma/dotfiles.git"
dotfiles_repo_version: master
dotfiles_repo_accept_hostkey: false
dotfiles_repo_local_destination: "~/Documents/dotfiles"

dotfiles_home: "~"
dotfiles_files:
  - .zshrc
  - .gitignore
  - .inputrc
  - .vimrc
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-dotfiles/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.git](https://galaxy.ansible.com/buluma/git)|[![Ansible Molecule](https://github.com/buluma/ansible-role-git/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-git/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-git.svg)](https://github.com/shadowwalker/ansible-role-git)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-dotfiles/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Amazon](https://hub.docker.com/r/buluma/amazonlinux)|all|
|[Alpine](https://hub.docker.com/r/buluma/alpine)|all|

The minimum version of Ansible required is 2.2, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-dotfiles/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-dotfiles/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-dotfiles/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)
