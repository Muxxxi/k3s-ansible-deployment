# Hetzner Deployment Repo


## Init Server 

```
ansible-playbook -i inventory  playbooks/init_ssh.yaml --extra-vars="host=hetzner02"
ansible-playbook -i inventory  playbooks/init_server.yaml --extra-vars="host=hetzner02 password=<password>"

```


## Create App Namespace

Create Namespace apps

```
kubectl create namespace apps
```

Create Issuer

```
kubectl create -f prod-issuer.yaml -n apps
kubectl create -f staging-issuer.yaml -n apps
```

# Install Monitoring 

Rancher Monitoring chart is based on:
https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

Now that we have Longhorn installed for Persistent Storage, we can install Monitoring with persistence. The Rancher Monitoring chart will install Prometheus, Grafana, Alert-Manager and other tools to monitor the cluster.

1. Login to the Rancher UI.
2. Go to Apps and Marketplace, Charts.
3. Click on Monitoring menu item and click Install.
3. Leave the version as the default, but select Customize Helm Options before Install at the bottom of the page. Click Next.
4. Under Prometheus (on the inner left column), change the following options:
    - Retention Size: 5GiB
    - CPU Limit: 1500m
    - Memory Limit 2048Mi
    - Select the box for Persistent Storage for Prometheus.
    - Size: 5Gi
    - Storage Class Name: longhorn
6. Under Grafana (on the inner left column), change the following options:
    - Select Enable with PVC Template
    - Size: 4Gi
    - Storage Class Name: longhorn
    - AccessMode: ReadWriteOnce

7. Click Next, then click Install.

Once this is complete, you should now have access to monitoring for your node and workloads running in your cluster.1. 


## Links

https://community.hetzner.com/tutorials/securing-ssh
https://community.hetzner.com/tutorials/install-ubuntu-2004-with-full-disk-encryption

https://cert-manager.io/docs/tutorials/acme/nginx-ingress/#step-6---configure-a-lets-encrypt-issuer
