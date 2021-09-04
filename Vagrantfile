Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant"
  

#############   Kafka Server   ##############
  config.vm.define "kafka" do |node|
    node.vm.box               = "generic/ubuntu2004"
    node.vm.box_check_update  = false
    node.vm.box_version       = "3.3.0"
    node.vm.hostname          = "kafka.example.com"
    node.vm.network "private_network", ip: "172.16.16.150"
    node.vm.provision "ansible_local" do |ans|
      ans.playbook = "kafka.yaml"
    end
    node.vm.provider :virtualbox do |v|
      v.name    = "kafka"
      v.memory  = 2048
      v.cpus    =  1
    end
  end

  
#############   Kubernetes Master Server   #############  
  config.vm.define "kmaster" do |node|
    node.vm.box               = "generic/ubuntu2004"
    node.vm.box_check_update  = false
    node.vm.box_version       = "3.3.0"
    node.vm.hostname          = "kmaster.example.com"
    node.vm.network "private_network", ip: "172.16.16.100"
    node.vm.provision "ansible_local" do |ans|
      ans.playbook = "kmaster.yaml"
    end
    node.vm.provider :virtualbox do |v|
      v.name    = "kmaster"
      v.memory  = 2048
      v.cpus    =  2
    end

  end

#############   Kubernetes Worker Nodes   #############  
  NodeCount = 1 

  (1..NodeCount).each do |i|

    config.vm.define "kworker#{i}" do |node|
      node.vm.box               = "generic/ubuntu2004"
      node.vm.box_check_update  = false
      node.vm.box_version       = "3.3.0"
      node.vm.hostname          = "kworker#{i}.example.com"
      node.vm.network "private_network", ip: "172.16.16.10#{i}"
      node.vm.provision "ansible_local" do |ans|
        ans.playbook = "kworker.yaml"
      end

  
      node.vm.provider :virtualbox do |v|
        v.name    = "kworker#{i}"
        v.memory  = 1024
        v.cpus    = 1
      end
    end
  end
end