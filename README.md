# kubectl service-tree

A `kubectl` plugin to explore the status for ingresses, services and their backends.

## Quick Start

```shell
# Install plugin
$ kubectl krew install service-tree

# Get help
$ kubectl service-tree --help

# Show ingresses, services and backends in `myapp` namespace
$ kubectl service-tree -n demo
Ingress demo.router (*/apache)
 Service demo.apache-service (3000)
 . Pod demo.apache-deployment-6f6846564b-dqp5c (172.18.0.6:80)
 . Pod demo.apache-deployment-6f6846564b-qqmth (172.18.0.8:80)

Ingress demo.router (*/nginx)
 Service demo.nginx-service (8080)
 . Pod demo.nginx-deployment-b486cddf6-x2wz4 (172.18.0.9:80)
    Container nginx
 x Pod demo.nginx-not-ready-deployment-55999bd676-b4mhk

Service demo.lb-service (6060)
. Pod demo.nginx-deployment-b486cddf6-x2wz4 (172.18.0.9:80)
   Container nginx
x Pod demo.nginx-not-ready-deployment-55999bd676-b4mhk

Service demo.nodeport-service (3030)
. Pod demo.apache-deployment-6f6846564b-dqp5c (172.18.0.6:80)
. Pod demo.apache-deployment-6f6846564b-qqmth (172.18.0.8:80)
```

## Notes

- Only services of type `NodePort` and `LoadBalancer` are displayed.

- When a Pod contains several containers and the containers declare their ports (with `ports.containerPort`), the name of the concerned container is displayed.
