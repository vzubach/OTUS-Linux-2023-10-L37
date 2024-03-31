Vagrant.configure("2") do |config|
    config.vm.box = "generic/centos8s"
    #config.vm.box_version = "2004.01"
 
    config.vm.provider :virtualbox do |v|
      v.memory = 2048
      v.cpus = 2
    end
  
    # Указываем имена хостов и их IP-адреса
    boxes = [
      { :name => "ipa.otus.lan",
        :ip => "192.168.57.10",
      },
      { :name => "client1.otus.lan",
        :ip => "192.168.57.11",
      },
      { :name => "client2.otus.lan",
        :ip => "192.168.57.12",
      }
    ]
    # Цикл запуска виртуальных машин
    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.hostname = opts[:name]
        config.vm.network "private_network", ip: opts[:ip]
      end
    end
    config.vm.provision "ansible" do |ansible|
      #ansible.verbose = "v"
      ansible.playbook = "ansible/provision.yml"
      ansible.host_key_checking = "false"
      ansible.compatibility_mode = "2.0"
      ansible.become = "true"
    end 
  end
