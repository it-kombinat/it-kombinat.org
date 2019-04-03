# Welcome to IT-Kombinat.org

## Splunk Demo

# Docker Demo


## Demo walkthrough


* [Docker Build](#Docker Build)
* [Docker for Ansible - Code Testing](#Docker for Ansible - Code Testing)
* [Splunk as Docker Container](#Splunk as Docker Container)
* [Kubernetes DEMO](# Kubernetes DEMO)

## Docker Build

# Clone the Build directory
```
git clone https://github.com/it-kombinat/ansible-centos.git
```
follow the instruction in the README.md

## Docker for Ansible - Code Testing
Download Ansible Code
```
git clone https://github.com/it-kombinat/ansible-os-hardening.git
```
Start Container with Volume attached
```
docker run --detach -v $(pwd)/ansible-os-hardening:/etc/ansible/roles/ansible-os-hardening:ro --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro stackware/ansible-centos /usr/lib/systemd/systemd
```
Get into the Container and run Ansible
```
docker exec -it <container-id> /bin/bash
```
Run Ansible-Playbook against Docker-Container - two times, for testing idempotent
```
docker exec <container-id>  ansible-playbook /etc/ansible/roles/ansible-os-hardening/default.yml --skip-tags sysctl,mount
```
# Splunk as Docker Container
Docker Container based on official Docker-Images by [Splunk)(https://github.com/splunk/docker-splunk)

## Before we start - Downloading Splunk apps
```
git clone https://github.com/it-kombinat/honeypot-app.git

git clone https://github.com/it-kombinat/itk-app.git
```
Starting docker container interactive to demonstrate content
```
docker run -it -v $(pwd)/honeypot-app:/opt/splunk/etc/apps/honeypot-app/ -v $(pwd)/itk-app:/opt/splunk/etc/apps/itk-app -p 8000:8000 -e "SPLUNK_PASSWORD=demo0815" -e "SPLUNK_START_ARGS=--accept-license" splunk/splunk:latest
```
Starting docker in dettached mode
```
docker run -d -v $(pwd)/honeypot-app:/opt/splunk/etc/apps/honeypot-app/ -v $(pwd)/itk-app:/opt/splunk/etc/apps/itk-app -p 8000:8000 -e "SPLUNK_PASSWORD=demo0815" -e "SPLUNK_START_ARGS=--accept-license" splunk/splunk:latest
```
show docker logs of dettached container
```
docker logs -f <container-id>
```
# Kubernetes DEMO
Kubernetes Service EKS provided by [AWS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html#eks-guestbook)
```
kubectl cluster-info

kubectl get nodes

kubectl get pods
```
## Launch Demo Application on EKS

* https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html#eks-guestbook
* https://kubernetes.io/docs/tutorials/stateless-application/guestbook/

## SpaaS with Snort (IDS) and Cowrie (Honeypot)
Second Demo - Deploying Splunk (SpaaS), Snort and Cowrie (Honeypot) with Ansible

Splunk as a Service with on-boarding of the following services
 - Badguy
 - Docker-Collector
 - SNORT
 - Cowrie (honeypot)

```
git clone https://github.com/it-kombinat/splunk-demo.git
```

**Presentation Slides**

[Splunk-Demo-Slides-Cowrie](https://it-kombinat.github.io/slides-splunk-snort/)


## Splunk Demo

Using the splunk demo by cloning the repository, further commands and instruction in README.md file.

```
git clone https://github.com/it-kombinat/splunk-demo.git
```

## Further steps:
- Downloading additional Ansible roles
- set up ansible variables for AWS
- running the Ansbile Play

**Presentation Slides**

[Splunk-Demo-Slides](https://it-kombinat.github.io/slides-splunk-demo/)
