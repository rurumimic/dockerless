# dockerless

- [CRI-O](https://cri-o.io/): Lightweight container runtime for Kubernetes
  - [Install](https://github.com/cri-o/cri-o/blob/master/install.md)
  - [Running kubernetes with CRI-O](https://github.com/cri-o/cri-o#running-kubernetes-with-cri-o)
- [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
- [kaniko](https://github.com/GoogleContainerTools/kaniko): Build Container Images In Kubernetes
  - [Introducing kaniko](https://cloud.google.com/blog/products/gcp/introducing-kaniko-build-container-images-in-kubernetes-and-google-container-builder-even-without-root-access)
- [microk8s](https://microk8s.io/)
  - [Docs](https://microk8s.io/docs)
  - [ubuntu/microk8s](https://github.com/ubuntu/microk8s)
- [Jenkins](https://www.jenkins.io/)
  - [Docs](https://www.jenkins.io/doc/book/)

---

## VM

- Ubuntu Server 20.04 LTS
- CPU: 2
- Memory: 4GB
- IP: `192.168.33.100`

## (Option) Add a enterprise CA as a trusted certificate authority

Add `*.cer`, `*.crt`, `*.pem` to `.gitignore`.  

`.cer` to `.crt`:
- `openssl x509 -inform DER -in before.cer -noout text`
- `openssl x509 -inform DER -in before.cer -out after.crt`

And copy certificates to `ca-trust` directory:

```bash
cp /path/to/enterprise.crt ./ca-trust
```

## Vagrant

- Vagrant: [Download](https://www.vagrantup.com/downloads)
- VirtualBox: [Download](https://www.virtualbox.org/wiki/Downloads)
- [Vagrantfile](Vagrantfile)

```bash
vagrant box add ubuntu/focal64 # --insecure
vagrant up
vagrant ssh
```

---

## Install CRI-O

- CRI-O github: [APT based operating systems](https://github.com/cri-o/cri-o/blob/master/install.md#apt-based-operating-systems)
- Kubernetes doc: [CRI-O](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#cri-o)




## Start a kubernetes cluster

---

## Deploy a service

### Build & push a container image

### Apply a service

```bash
kubectl apply -f /k8s/nginx/configmap.yaml -f /k8s/deployment.yaml
```

---

## Test

On the host machine: [http://192.168.33.100:30080](http://192.168.33.100:30080)

## Delete a service

```bash
kubectl delete -f /k8s/nginx/configmap.yaml -f /k8s/deployment.yaml
```

---

## Jenkins

### Install Jenkins

### Create a pipeline

### Commit

---

## Clean up VM

```bash
vagrant halt
vagrant destroy -f
```