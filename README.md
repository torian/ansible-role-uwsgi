# Ansible role for uWSGI

[![Build Status](https://travis-ci.org/torian/ansible-role-uwsgi.svg)](https://travis-ci.org/torian/ansible-role-uwsgi)

This role will install [uWSGI](https://uwsgi-docs.readthedocs.org/en/latest/).

## Tested on

  * Ubuntu trusty

## Defaults

  * `uwsgi_version`: 2.0.15
  * `uwsgi_user`: uwsgi
  * `uwsgi_group`: uwsgi
  * `uwsgi_logfile`: /var/log/uwsgi/uwsgi.log
  * `uwsgi_master_fifo`: /var/run/uwsgi/master.fifo

You are free to configure daemon settings as you wish, but some
defaults are defined for you:

  * `uwsgi_daemon_config_defaults`
    * `uid`: `uwsgi_user`
    * `gid`: `uwsgi_group`
    * `daemonize`: `uwsgi_logfile`
    * `master-fifo`: `uwsgi_master_fifo`

## Usage

### Vassals

```
---
- hosts: localhost

  vars:
    - uwsgi_vassals_enabled: True
    - uwsgi_vassals:
       some_app:
          enabled: True
          http-socket: ':5000'
          processes: 1
          listen: 64
          wsgi-file: /some/app/wsgi.py
        another_app:
          enabled: True
          socket:  "{{uwsgi_socket_dir}}/another_app.socket"
          
        
  roles:
    -  ansible-role-uwsgi

```

