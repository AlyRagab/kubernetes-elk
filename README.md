Kubernetes ELK stack
===

This sets up a pod with ElasticSearch, Logstash, and Kibana that is run as a StatefulSet with persistent storage.

Filebeat is run on each node as a DaemonSet.


## Installation

To set up, first install the `elk` namespace.
```
kubectl --kubeconfig=kubeconfig apply -f namespace-elk.json
```

Then install the storage class.
```
kubectl --kubeconfig=kubeconfig apply -f sc.yaml
```

Then install the elk pod and services.
```
kubectl --kubeconfig=kubeconfig apply -f elk-deployment.yaml
kubectl --kubeconfig=kubeconfig apply -f logstash-service.yaml
kubectl --kubeconfig=kubeconfig apply -f kibana-service.yaml
```

Finally install the filebeat daemon.
```
kubectl --kubeconfig=kubeconfig apply -f filebeat-daemonset.yaml
```

## Viewing kibana

To load kibana you have to ssh tunnel to any of the nodes.
```
ssh -L30601:172.16.25.47:30601 -N occ-dev-kube
```

and then point your web-browser to
```
http://localhost:30601/
```
