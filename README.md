# vagranetes
Combination of Vagrant and Ansible to spin up a Kubernetes cluster. Supporting different CNIs.


TODO:
Add support for MetalLB and other 3rd ingress providers.
Restrict permissions on /home/vagrant/.kube/config
Add Cilium Binary support 
Request user input for CNI

### Prerequisites
- Vagrant
- Ansible

### Configuration
#### Define CNI 
in lib/vars/vars_file.yml
```
cni: calico
cni: flannel
```

#### Define Kubernetes version current default 1.28.2-00
in lib/vars/vars_file.yml
```
kubeversion: 1.28.2-00
```

#### Define amount of nodes
in Vagrantfile:
```
N = 2
```


### Spin up cluster
```
$ vagrant up
```

### Verify on master
```
$ vagrant ssh k8s-master
$ kubectl get nodes
NAME         STATUS   ROLES                  AGE     VERSION
k8s-master   Ready    control-plane,master   5m6s    v1.23.0
node-1       Ready    <none>                 2m59s   v1.23.0
node-2       Ready    <none>                 68s     v1.23.0
```
