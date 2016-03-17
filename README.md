# Redis

Just a simple Redis setup for minimum of fuss. For clustering it's probably worth to create separate playbook.

## TODO

- Authorization

## Requirements

Ansible version 2.0.0.2

## Platforms

- Ubuntu

## Role Variables

Variable name         | Default                                   | Description
:-------------------- | :---------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
redis_bind            | <not set>                                 | Ip address to bind to.
redis_port            | 6379                                      | redis port number
redis_pidfile         | /var/run/redis.pid                        | redis pidfile path
redis_daemonize       | yes                                       | Should be string "yes" or "no", or else it will produce True/False in configuration, which will violate syntax of Redis config.
redis_timeout         | 100                                       | Close connection after client's N seconds idling (0 to disable)
redis_keepalive       | 0                                         | Check defaults/main.yml for explanation
redis_loglevel        | notice                                    | Available log levels: debug, verbose, notice, warning
redis_logfile         | /var/log/redis/redis-server.log           | Path to logfile
redis_syslog          | no                                        | Enabling syslog. Should be string "yes" or "no"
redis_syslog_ident    | redis                                     | Specify syslog identity
redis_syslog_facility | local0                                    | Specify the syslog facility. Must be USER or between LOCAL0-LOCAL7.
redis_databases       | 16                                        | Set the number of databases. The default database is DB 0, you can select a different one on a per-connection basis using SELECT <dbid> where dbid is a number between 0 and 'databases'-1
redis_backup_save     | - "900 1"<br>  - "300 10"<br> - "60 1000" | In this example the behaviour will be to save after 900 sec (15 min) if at least 1 key changed after 300 sec (5 min) if at least 10 keys changed after 60 sec if at least 1000 keys changed
redis_max_clients     | 10000                                     | Set the max number of connected clients at the same time. By default this limit is set to 10000 clients, however if the Redis server is no able to configure the process file limit to allow for the specified limit the max number of allowed clients is set to the current file limit minus 32 (as Redis reserves a few file descriptors for internal uses). <br> Once the limit is reached Redis will close all the new connections sending an error 'max number of clients reached'.

## Example

```
- hosts: redis
  remote_user: root
  become: yes
  become_method: sudo

  vars:
    - redis_bind: 10.128.15.177

  roles:
    - { role: redis }
```

## License

MIT

## Author Information

Roman Gorodeckij ([holms@holms.lt](mailto:holms@holms.lt)) John Brooker (jb-github@outlook.com)

## License

MIT

## Author Information

Roman Gorodeckij ([holms@holms.lt](mailto:holms@holms.lt))
