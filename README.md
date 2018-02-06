[![Build Status](https://travis-ci.org/while-true-do/ansible-role-nginx.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-nginx)

# Ansible Role: nginx
| A role to install and configure nginx.

nginx web server will be installed, enabled and started.
A basic configuration file without virtual hosts is deployed.

## Motivation

This role is needed to setup nginx.

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while-true-do/nginx)

```
ansible-galaxy install while-true-do.nginx
```

Install from [Github](https://github.com/while-true-do/ansible-role-nginx)

```
git clone https://github.com/while-true-do/ansible-role-nginx.git while-true-do.nginx
```

## Requirements

Used Modules:

-   [file](http://docs.ansible.com/ansible/latest/file_module.html)
-   [package](http://docs.ansible.com/ansible/latest/package_module.html)
-   [service](http://docs.ansible.com/ansible/latest/service_module.html)
-   [template](http://docs.ansible.com/ansible/latest/template_module.html)

## Dependencies

This role depends on the below roles. You have to install them:

-   [repo-epel](https://github.com/while-true-do/ansible-role-repo-epel)

```
ansible-galaxy install -r requirements.yml
```

## Role Variables


```yaml
# defaults/main.yml
---
# You can change the state (present|absent)
wtd_nginx_state: "present"

wtd_nginx_packages: ["nginx"]

wtd_nginx_conf_path: "/etc/nginx"
wtd_nginx_vhost_path: "/etc/nginx/conf.d"

# Config
wtd_nginx_user: "nginx"

wtd_nginx_error_log: "/var/log/nginx/error.log"

# loglevel can be: debug, info, notice, warn, error, crit, alert, or emerg
wtd_nginx_error_log_loglevel: "error"
wtd_nginx_access_log_main: "/var/log/nginx/access.log"
wtd_nginx_access_log_main_log_format: |
  '$remote_addr - $remote_user [$time_local] "$request" '
  '$status $body_bytes_sent "$http_referer" '
  '"$http_user_agent" "$http_x_forwarded_for"'

# don't show nginx version per default:
wtd_nginx_server_tokens: "off"

wtd_nginx_pidfile: "/run/nginx.pid"
wtd_nginx_worker_processes: "1"
wtd_nginx_mime_file_path: "/etc/nginx/mime.types"

wtd_nginx_worker_connections: "1024"

wtd_nginx_sendfile: "on"
#wtd_nginx_hash_bucket_size: "128"
#wtd_nginx_tcp_nopush: "on"
#wtd_nginx_gzip: "on"

wtd_nginx_keepalive_timeout: "65"

wtd_nginx_proxy_cache_path: ""
```

## Example Playbook

Simple Example:

```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.nginx }
```

Advanced Example:

```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.nginx, wtd_nginx_worker_processes: "8", wtd_nginx_tcp_nopush: "on" }
```

## Testing

All tests are located in [test directory](./tests/).

Basic testing:

```
bash ./tests/test-spelling.sh
bash ./tests/test-ansible.sh
```

## Contribute / Bugs

Thank you so much for considering to contribute. Every contribution helps us.
We are really happy, when somebody is joining the hard work. Please have a look 
at the links first.

-   [Contribution Guidelines](./docs/CONTRIBUTING.md)
-   [Create an issue or Request](https://github.com/while-true-do/ansible-role-nginx/issues)
-   [See who was contributing already](https://github.com/while-true-do/ansible-role-nginx/graphs/contributors)

## License

This work is licensed under a [BSD License](https://opensource.org/licenses/BSD-3-Clause).

## Author Information

Blog: [blog.while-true-do.org](https://blog.while-true-do.org)

Mail: [hello@while-true-do.org](mailto:hello@while-true-do.org)
