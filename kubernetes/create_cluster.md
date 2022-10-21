# **Building a Kubernetes Cluster**


![Kubernetes](https://www.stackxperts.com/wp-content/uploads/2020/01/k8s-logo.png)
## *I'm going to create three servers, one for the control plane and two for worker nodes.*

3 Servers:
              
Distribution: Ubuntu 20.04 Focal Fossa LTS

Size: Medium

Names:
              
1- k8s_control_plane

2- k8s_worker_node1

3- k8s_worker_node2


Steps: 

Set hostnames for each server so they are easy to identify since I'll be working in all of them at the same time

```

sudo hostnamectl set-hostname k8s-control   #in server k8s_control_plane

sudo hostnamectl set-hostname k8sworker1    #in server k8s_worker_node1

sudo hostnamectl set-hostname k8sworker2    #in server k8s_worker_node2

```

On all nodes I set up the hosts file to enable all the nodes to reach each other using these hostnames. I did this by editing /etc/hosts.
        
```

sudo vi /etc/hosts

```
<img width="481" alt="k8s_two" src="https://user-images.githubusercontent.com/94250541/197082128-c05b0949-d074-4685-803e-7e66b14c7233.png">
Note, I originally entered the names incorrectly (shown here) and went back to fix them.


I then logged out of all the servers and logged back in.
      
<img width="579" alt="k8s_three" src="https://user-images.githubusercontent.com/94250541/197082431-7b69a852-3fe8-4834-a062-9c79d302d1e2.png">

Next I added containerd to all the servers, including some specific settings:
              
```

cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF

sudo modprobe overlay   #modprobe will immediately enable these kernal modules without restarting the server

sudo modprobe br_netfilter  #everytime the servers start, these modules will be enabled

cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf   #set up some system level configs
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

sudo sysctl --system   #apply configurations

```

<img width="947" alt="k8s_nine" src="https://user-images.githubusercontent.com/94250541/197107346-1b25d03d-af10-4ca7-846e-c91652462252.png">

Installed and configured containerd

```

sudo apt-get update && sudo apt-get install -y containerd
sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd

```

<img width="562" alt="k8s_four" src="https://user-images.githubusercontent.com/94250541/197096445-77323562-3c82-4786-bd2f-da3648ce7d60.png">
<img width="565" alt="k8s_five" src="https://user-images.githubusercontent.com/94250541/197096324-3871b6cc-def3-46c3-92de-08d1edd10439.png">

Disabled swap #currently swap is not supported and can affect performance

<img width="478" alt="k8s_six" src="https://user-images.githubusercontent.com/94250541/197106675-9b596f8a-974d-45a6-96fa-0b7940d3f7e7.png">


Installed  kubeadm, kubelet, and kubectl on all nodes

```

sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt-get update

```

<img width="473" alt="k8s_seven" src="https://user-images.githubusercontent.com/94250541/197096591-fc868a37-09c9-4412-88c8-fe28911648b9.png">

```

sudo apt-get install -y kubelet=1.24.0-00 kubeadm=1.24.0-00 kubectl=1.24.0-00
sudo apt-mark hold kubelet kubeadm kubectl

```

<img width="469" alt="k8s_eight" src="https://user-images.githubusercontent.com/94250541/197096624-6c24f068-2f87-41fe-a155-478b6ba7f886.png">

It failed at first because I was missing a space.

Then I initialized the cluster and set up kubectl access only on the control plane.

<img width="770" alt="k8s_ten" src="https://user-images.githubusercontent.com/94250541/197107093-a1665793-b768-4795-b58f-c04b93e66af8.png">

<img width="758" alt="k82_11" src="https://user-images.githubusercontent.com/94250541/197107558-b9beeadf-dd36-4c2a-8816-f2254fbf6860.png">

Used the command per init instructions and verified node

<img width="482" alt="k82_12" src="https://user-images.githubusercontent.com/94250541/197107563-f0dde17e-3d83-4213-b618-caa49dedfeaa.png">

Installed the Calico network add-on
```

kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

```

Used the token to join worker nodes 1 and 2 
<img width="960" alt="k8s_13" src="https://user-images.githubusercontent.com/94250541/197107589-8c52288e-0d6e-4502-95f1-274787332d86.png">

<img width="445" alt="k82_14" src="https://user-images.githubusercontent.com/94250541/197107606-c0f47970-9cfd-4df9-94c2-cbbbcc114140.png">



