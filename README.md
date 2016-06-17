# Demo service discovery

## Synopsis

```bash
vagrant up
vagrant ssh sudo su root
docker exec -it testwebservice_nginx_ctmpl_1 cat /etc/nginx/conf.d/default.conf|grep 'web-1;'
docker kill testservice1_testwebservice_1
docker exec -it testwebservice_nginx_ctmpl_1 cat /etc/nginx/conf.d/default.conf|grep 'web-1;'
```

## Description

A demo project showing some service discovery. Based on

* consul
* gliderlabs/registrator
* consul-template

Basically, each time a container with an exposed port gets started
registrator reports the service to consul.
Consul gets polled in a 1s interval by consul-template which then creates
a nginx.conf based on the information from Consul. When the nginx.conf changes,
consul-template reloads nginx.

consul-template only uses services that have a ``SERVICE_TAGS: http`` label.

## LICENSE

AGPv3

## Sources

* https://www.airpair.com/scalable-architecture-with-docker-consul-and-nginx
* https://github.com/hashicorp/consul-template

## Authors

* Alvaro Aleman
