# Install docker, kubenetes and fix network issue for Deepin os

## Install Docker

### Update software repositories

```bash
sudo apt update -y
```

### Uninstall old version of docker

```bash
dpkg -l | grep -i docker
sudo apt-get purge -y docker-engine docker docker.io docker-ce  
sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce  
# Remove docker folder manually
sudo rm -rf /var/lib/docker /etc/docker
sudo groupdel docker
sudo rm -rf /var/run/docker.sock
```

### Install required package 

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

### Add the GPG key for the official Docker repository to your system

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

### Add the Docker repository to APT sources

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

> If you install Docker from Deepin os 15.11, run the following command before add Docker repository

```bash
sudo vim /usr/share/python-apt/templates/Deepin.info
```

> and change `Suite: unstable` to `Suite: stable`

### Install docker-ce

```bash
sudo apt update -y
sudo apt install docker-ce
```

### Check docker service status

```bash
sudo service docker status
# or
sudo systemctl docker status
```

### Config to use Docker without sudo

```bash
sudo usermod -aG docker ${USER}
su - ${USER}
id -nG
```

## Install Kubenetes

### Add Google cloud GPG key

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```

### Add repository

```bash
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

### Install kubeadm

```bash
sudo apt install kubeadm
```

### Disable swap

```bash
sudo swapoff -a
```

## Init cluster

```bash
sudo kubeadm init
```

### Config kubectl

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl get pods --all-namespaces
```

> If you install Kubenetes from Deepin os and docker container cannot access internet, run the command below

```bash
sudo apt remove apparmor -y
```

## Install minikube

> Make sure you installed kubectl and have a hypervisor installed such as: KVM, Virtualbox
>
> Minikube also supports a `--driver=none` option that runs the Kubernetes components on the host and not in a VM. Using this driver requires Docker and a Linux environment but not a hypervisor.

### Install Minikube via direct download

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
sudo mkdir -p /usr/local/bin
sudo install minikube /usr/local/bin
```

### Start minikube

```bash
minikube start
```

