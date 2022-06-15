# goSDN  - Infrastructure as Code

# Ansible
## Disclaimer: 
Please note that these playbooks were tested on Ubuntu 20.04 LTS and Debian 10 and **may not work** on other Debian/Ubuntu versions.

# Dependencies

Install Docker collection with ansible-galaxy

```
ansible-galaxy collection install -r requirements.yaml
```

Configure your hosts in hosts.yaml or the playbooks will not work!\
Also add your public keys for login into roles\add-ssh-key-root\keys !

# Usage

## Install

```
ansible-playbook -i hosts.yaml init.yaml
```

## Update

```
ansible-playbook -i hosts.yaml update.yaml
```

## Reboot

```
ansible-playbook -i hosts.yaml reboot.yaml
```

# Gitlab Runner

The variables (**GITLAB_URL** and **REGISTRATION_TOKEN**) are found in the GitLab project under Settings -> CI/CD -> Runners -> Specific runners  
Shared runners **should** then be disabled for the project.

## Register Runner

```
ansible-playbook -i hosts.yaml register-gitlab-runner.yaml --extra-vars "runner_host=<GITLAB_URL> runner_secret=<REGISTRATION_TOKEN>"
```

DOCKER_PRIVILEGED

## Unregister Runner

```
ansible-playbook -i hosts.yaml unregister-gitlab-runner.yaml --extra-vars "runner_name=<RUNNER_NAME>"
```

# Optional: Change Docker directory

```
ansible-playbook -i hosts.yaml change-docker-root-dir.yaml --extra-vars "docker_old_path=<DOCKER_OLD_PATH> docker_new_path=<DOCKER_NEW_PATH>"
```

## e.g.

```
ansible-playbook -i hosts.yaml change-docker-root-dir.yaml --extra-vars "docker_old_path=/var/lib/docker docker_new_path=/mnt/fastNbig/docker"
```
