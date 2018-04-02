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
  
`nginx_container_name`
Name of docker container

`nginx_allow`
List of IP addresses to allow to server.

`nginx_dir`
Nginx base dir. (_default: /tmp/nginx_)

`nginx_htpasswd`
List of htpasswd.

`nginx_openssl_dhparam_numbits`
Num bits for generate dhparam cert. (_default: 4096_)

`nginx_container_options`
Options for run docker container. Default:
```yaml
  image: "nginx:alpine"
  expose: []
  log_driver: "syslog"
  log_options:
    tag: "{{nginx_container_name}}"
  ports:
    - 443:443
    - 80:80
  volumes: []

```

Add role to project:
----------------
Add role into your requirements(_requirements.yml_ for example):
```yaml
- src: https://github.com/lexa-uw/ansible-role-nginx-in-docker
  version: v1.0.0
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
nginx_container_options:
  image: "nginx:1.13.10-alpine"
  expose: []
  log_driver: "syslog"
  log_options:
    tag: "nginx-tag"
  ports:
    - 443:443
    - 80:80
  volumes: []
```

