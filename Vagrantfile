IMAGE_NAME = "bento/ubuntu-20.04"
N = 2

# Kubernetes Version
kube_ver_setting = "1.28.2-00"
# CNI Settings - flannel or calico supported
cni_setting = "flannel" 
# CIDR - Default supported by flannel and calico 
cidr_var = "192.168.0.0/16"

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end
      
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.56.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "lib/master-playbook.yml"
            ansible.extra_vars = {
              cni: cni_setting,
              kubeversion: kube_ver_setting,
              cidr: cidr_var
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.56.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "lib/node-playbook.yml"
                ansible.extra_vars = {
                  cni: cni_setting,
                  kubeversion: kube_ver_setting,
                  cidr: cidr_var
                }
            end
        end
    end
end
