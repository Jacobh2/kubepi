# kubepi
Kuberentes on Raspberry Pi

---
##### Step 1.
Install Hypriot on an SD card (https://blog.hypriot.com/downloads/)

username: `pirate`
password: `hypriot`
##### Step 2.
Set the hostname of the node:
`sudo nano /boot/device-init.yaml`
##### Step 3.
Change to root: `sudo su -`
##### Step 4. 
`curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -`

`echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list`

`apt-get update && apt-get install -y kubeadm`

#### For master: 
##### Step 1.
`kubeadm init --pod-network-cidr 10.244.0.0/16`
##### Step 2. 
`curl -sSL https://rawgit.com/coreos/flannel/master/Documentation/kube-flannel.yml | sed "s/amd64/arm/g" | kubectl create -f -`
#### For slaves:
##### Step 1:
`kubeadm join --token <token> <master-ip>`

---
##### To reset:
`kubeadm reset`

##### To run pods on master:
`kubectl taint nodes --all dedicated-`
