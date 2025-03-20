Vagrant.configure("2") do |config|
    # Configuração geral das VMs
    config.vm.box = "generic/rocky8"
  
    # Criando a máquina Master
    config.vm.define "master" do |master|
      master.vm.hostname = "master"
      master.vm.network "private_network", ip: "172.89.57.10"
      master.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 2
      end

      master.ssh.insert_key = false
      master.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"

      master.vm.provision "shell", inline: <<-SHELL
      dnf update -y
        dnf install -y vim net-tools
        echo "Master is ready!"
      SHELL
    end
  
    # Criando os Nodes (3 máquinas)
    (1..3).each do |i|
      config.vm.define "node#{i}" do |node|
        node.vm.hostname = "node#{i}"
        node.vm.network "private_network", ip: "172.89.57.1#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "1024"
          vb.cpus = 1
        end

        node.ssh.insert_key = false
        node.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
        node.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
        
        node.vm.provision "shell", inline: <<-SHELL
          dnf update -y
          dnf install -y vim net-tools
          echo "Node#{i} is ready!"
        SHELL
      end
    end
  end
  