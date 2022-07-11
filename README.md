# ansible-traefik-redis-service

A little ansible role that will create [traefik configuration in redis][0].

Useful for when you want to dynamically manage the traefik configuration, but do
not want to let traefik have access to your docker/podman socket.

## Prerequisites

* [`community.general` collection][2] (for the redis module)
* `redis-cli` installed on the host that the playbook is running on

## Usage:

See the test file at [./molecule/default/converge.yml][1] for an example of how to use it.

That test file produces an equivelent configuration in redis of:

```
traefik.enable=true
traefik.http.routers.router-http-mything_mydomain_com_foo.rule=Host(`mything.mydomain.com`)
traefik.http.routers.router-http-mything_mydomain_com_foo.service=mything_mydomain_com_foo
traefik.http.routers.router-http-mything_mydomain_com_foo.entrypoints.0=secure
traefik.http.routers.router-http-mything_mydomain_com_foo.service=mything_mydomain_com_foo
traefik.http.services.mything_mydomain_com_foo.loadbalancer.servers.0.url=http://mything:80
traefik.http.services.mything_mydomain_com_foo.loadbalancer.serverstransport=ignorecert@file
```


## License

ansible-role-traefik-redis-service

Copyright (C) 2022 Casey Link

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

[0]: https://doc.traefik.io/traefik/providers/redis/
[1]: ./molecule/default/converge.yml
[2]: https://galaxy.ansible.com/community/general
