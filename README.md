Ansible role for setup and run [Nginx](http://nginx.org/) server in [Docker](https://www.docker.com/) container. 
============

This role will allow you to install Nginx server on your own Docker node.
With nginx SSL/TLS configuration for "A+" Qualys SSL Labs rating by default.

Requirements
------------

This role requires Ansible 2.5 or higher.

Role Variables
--------------

### Package options:
  
`nginx_global_config`
Template for global config file

`nginx_allow`
List of IP addresses to allow to server.

`nginx_dir`
Nginx base dir. (_default: /tmp/nginx_)

`nginx_htpasswd`
List of htpasswd.

`nginx_openssl_dhparam_numbits`
Num bits for generate dhparam cert. (_default: 4096_)

#### Container options
Options for run docker container. Default:
```yaml
nginx_container_command: []
nginx_container_env: {}
nginx_container_image: "nginx:alpine"
nginx_container_log_driver: "json-file"
nginx_container_name: "nginx"
nginx_container_network_mode: bribge
nginx_container_networks: []
nginx_container_pull: "yes"
nginx_container_recreate: "no"
nginx_container_restart_policy: "always"
nginx_container_restart: "no"
nginx_container_state: "started"
nginx_container_volumes: []
nginx_container_log_options: {
  labels: "{{ nginx_container_name }}",
}
nginx_container_ports:
  - 443:443
  - 80:80

```

Add role to project:
----------------
Add role into your requirements(_requirements.yml_ for example):
```yaml
- src: https://github.com/lexa-uw/ansible-role-nginx-in-docker
  version: v1.3.0
  name: nginx
```

Install role: `ansible-galaxy install -r ./requirements.yml --roles-path ./roles/`
Playbook example:
----------------
```yaml
- hosts: all
  vars_files:
    - vars/main.yml
  roles:
    - { role: nginx }
```

Inside `vars/main.yml`
```yaml
nginx_container_name: my-own-nginx-container
nginx_allow:
  - "127.0.0.1"
  - "1.1.1.1"
nginx_dir: "{{ansible_env.PWD}}/docker/nginx"
nginx_htpasswd:
  - "admin:$apr1nuGQ0aW41nBe8nisbHRz4JZ9vq43u"
nginx_openssl_dhparam_numbits: 4096

nginx_container_image: "nginx:1.15.9-alpine"
nginx_container_name: "nginx"
nginx_container_network_mode: "host"
nginx_container_ports: []

```
