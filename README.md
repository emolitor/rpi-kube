# rpi-kube
Creates a k3s Kubernetes cluster on one or more Raspberry Pi SBCs. By default 
it deviates from standard K3s and does not install Traefik Ingress or Klipper 
LB as I prefer to manually install Ingress and LB. By default it creates a 
Kubernetes config file named kubeconfig which you can use with kubectl.

## Setup
```shell
ansible-galaxy install -r requirements.yml
```

## Setup
Create your inventory file. The example below assumes you are using 
[Lite ARM64](https://downloads.raspberrypi.org/raspios_lite_arm64/images/)
Raspberry PI OS image using the default username and password. This is not 
secure but good enough for home lab usage. You designate your server/control 
node using the k3s_control_node varible.
```dosini
10.0.0.10 ansible_python_interpreter=python3 ansible_user=pi ansible_password=raspberry k3s_control_node=true
10.0.0.11 ansible_python_interpreter=python3 ansible_user=pi ansible_password=raspberry
10.0.0.12 ansible_python_interpreter=python3 ansible_user=pi ansible_password=raspberry
10.0.0.13 ansible_python_interpreter=python3 ansible_user=pi ansible_password=raspberry
```

## Provision
```shell
ansible-playbook playbook/k3s.yml -i inventory/hosts.ini
```

## Configure kubectl
```shell
mkdir -p ~/.kube
cp kubeconfig ~/.kube/config
```
