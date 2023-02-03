# K3s-ansible-deployment
Bootstrap k3s instance on hetzner with a bunch of ansible playbooks for useful applications


## Init Server 

```
ansible-playbook -i inventory  playbooks/init_ssh.yaml --extra-vars="host=hetzner02"
ansible-playbook -i inventory  playbooks/init_server.yaml --extra-vars="host=hetzner02 password=<password>"
```


## Links

https://community.hetzner.com/tutorials/securing-ssh
https://community.hetzner.com/tutorials/install-ubuntu-2004-with-full-disk-encryption
https://cert-manager.io/docs/tutorials/acme/nginx-ingress/#step-6---configure-a-lets-encrypt-issuer
