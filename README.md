# Grafana K8

Configuration files for running grafana as a pod in a kubernetes cluster.  I am using raspberry pi 4 configured
as a microk8 cluster.

## Getting Started
### Prerequisites

- [MicroK8s](https://microk8s.io/) for our kubernetes cluster

For microk8s, make sure the following add-ons are enabled:
- cert-manager
- dns
- ingress
- metallb

I keep all my cluster storage on a NAS server.  I expose the storage via an nfs mount that the cluster
can access.  You will need to install the nfs-csi driver.

### Installing

We need to setup a grafana namespace in our microk8 cluster.

    kubectl apply -f grafana-namespace.yaml

Next we need to provision storage by making a persistent volume claim

    kubectl apply -f grafana-pvc.yaml

This step creates the kubernetes grafana pod.

    kubectl apply -f grafana-deployment.yaml

Creating a service allows outside access to the grafana pod. This 
service file is setup to use the metallb load balancer. 

    kubectl apply -f grafana-service.yaml

If all goes well, you should be able to use the external load
balancer ip address in your browser to access the grafana dashboard.

## Built With

  - [MicroK8s](https://microk8s.io/) - Used as the kubernetes cluster software
  - [Raspberry Pi](https://www.raspberrypi.com/) - Use as the compute host infrastructure

