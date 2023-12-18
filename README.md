# k8s-lab

Kubernetes lab with 1 control plane and 2 worker nodes

FYI: *Kubernetes === k8s === K8s*

This is a K8s setup I am using to test on my dev environments, either locally (on Hyper-V) or on a separate box (Proxmox VMs).

The whole setup consists of 1 control plane node (2 vCPUs, 4 GB RAM, 30 GB disk) and 2 worker nodes (2 vCPUs, 2 GB RAM, 30 GB disk).

## My Environment specifics

* Local hosts are on 192.168.68.0/24 subnet
* All 3 hosts running latest Ubuntu 20.04 LTS (to be upgraded to 22.04 LTS at some point)
* Local user: robertas
* `~/.ssh/config` file has the following:
```
Host k8s-control
        HostName 192.168.68.16
        User robertas

Host k8s-worker1
        HostName 192.168.68.17
        User robertas

Host k8s-worker2
        HostName 192.168.68.18
        User robertas
```
* I ran `ssh-copy-id robertas@k8s-control` (and the worker nodes) - for ease of access to hosts
* I also update sudoers file with `sudo visudo` on each host with below so I don't need password on every sudo. **! ! ! DEVELOPMENT ONLY ! ! !**
```
# from:
%sudo   ALL=(ALL:ALL) ALL

# to:
%sudo   ALL=(ALL:ALL) NOPASSWD: ALL
```

## Ansible

The few manual steps above is the only thing I've done manually, everything else is either ansible, or further down the line.

### group_vars/all.yml

Variables for all nodes

### inventory/lab.yml

Contains all the details about your environment.

Has 3 groups in it:

* k8s - all nodes
* control - K8s control plane node
* worker - K8s worker nodes

**! ! !**

`k8s-control` is used in ansible as host name, so better not change it in inventory file.

### common.all.yml

Update packages to the latest version, add some bash aliases and bash completion for kubeadm and kubectl

```bash
ansible-playbook -i inventories/lab.yml common.all.yml
```

### k8s.yml - setup

Run initial setup steps to prepare nodes:

* Kernel modules
* Sysctl config
* Disable swap
* Add docker repo to apt
* Install containerd.io
* Add kubernetes repo to apt
* Install and hold kubeadm, kubectl and kubelet
* REBOOT

```bash
ansible-playbook -i inventories/lab.yml k8s.yml -t setup
```

### k8s.yml - init

Initialize K8s cluster:

```bash
ansible-playbook -i inventories/lab.yml k8s.yml -t init
```

### k8s.yml - join

Join worker nodes to the K8s cluster:

```bash
ansible-playbook -i inventories/lab.yml k8s.yml -t join
```
