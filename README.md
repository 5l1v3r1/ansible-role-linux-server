# Linux server role

Role that install a generic setup for a Debian linux:

 - Docker
 - Monitoring with prometheus (node exporter + cAdvisor)
 - Kernel parameters
 - Basic tools and packages
 - Import of ssh keys and gpg keys from github
 
# Example playbook

This is an example playbook


```yml
- hosts: all
  vars:
    hostname: "template"
    domain: "strm.sh"
    network:
      ip: "192.168.0.9"
      cidr: "/24"
      gateway: "192.168.0.1"
      dns: "8.8.8.8"
    static_hosts: "{{ lookup('file', 'hosts') }}"
    github_user: opsxcq
  tasks:
  - debug:
        msg: "Your other tasks here"
  roles:
    - ../..
```

Optional variables:

 - `network.cidr`: default value is `/24`
 - `static_hosts`: if not present, won't change `/etc/hosts`

# Requirements file

```yml
- src: git+https://github.com/opsxcq/ansible-role-linux-server.git
  name: "opsxcq.linux_server"
```

# Tmux configuration

Tmux is added to this setup, but with a difference that it uses `Ctrl+A`, so you
can keep a tmux session (using `Ctrl+B`) locally connected to a tmux remotely.
