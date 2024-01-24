
[0;1;35;95m┌─[0;1;31;91m──[0;1;33;93m──[0;1;32;92m──[0;1;36;96m──[0;1;34;94m─┐[0m
[0;1;31;91m│v[0;1;33;93mag[0;1;32;92mra[0;1;36;96mne[0;1;34;94mte[0;1;35;95ms│[0m
[0;1;33;93m└─[0;1;32;92m──[0;1;36;96m──[0;1;34;94m──[0;1;35;95m──[0;1;31;91m─┘[0m

# vagrant-ansible-kubernetes
Combination of Vagrant and Ansible to spin up a Kubernetes cluster

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
