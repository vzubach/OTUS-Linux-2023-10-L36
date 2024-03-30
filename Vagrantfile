Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |v|
	  v.memory = 1024
    v.cpus = 2
  end
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "vvv"
    ansible.playbook = "ansible/playbook.yml"
    ansible.host_vars = {
        "inetRouter" => {"bond_ip" => "192.168.255.1"},
        "centralRouter" => {"bond_ip" => "192.168.255.2"},
        "testClient1" => {"vlan_id" => 1, "vlan_ip" => "10.10.10.254"},
        "testServer1" => {"vlan_id" => 1, "vlan_ip" => "10.10.10.1"},
        "testClient2" => {"vlan_id" => 2, "vlan_ip" => "10.10.10.254"},
        "testServer2" => {"vlan_id" => 2, "vlan_ip" => "10.10.10.1"}
    }
    #ansible.inventory_path = "ansible/hosts"
    #ansible.limit = "all"
    ansible.host_key_checking = "false"
    ansible.become = "true"
  end

  config.vm.define "inetRouter" do |inetRouter|
    inetRouter.vm.box = "centos/7"
    inetRouter.vm.box_version = "2004.01"
    inetRouter.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
    inetRouter.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
    inetRouter.vm.network "private_network", adapter: 8, ip: "192.168.56.10"
    inetRouter.vm.hostname = "inetRouter"
  end

  config.vm.define "centralRouter" do |centralRouter|
    centralRouter.vm.box = "centos/7"
    centralRouter.vm.box_version = "2004.01"
    centralRouter.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
    centralRouter.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
    centralRouter.vm.network "private_network", adapter: 6, ip: '192.168.255.9', netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
    centralRouter.vm.network "private_network", adapter: 8, ip: '192.168.56.11'
    centralRouter.vm.hostname = "centralRouter"
  end

  config.vm.define "office1Router" do |office1Router|
    office1Router.vm.box = "centos/7"
    office1Router.vm.box_version = "2004.01"
    office1Router.vm.network "private_network", adapter: 2, ip: '192.168.255.10',  netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
    office1Router.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "vlan1"
    office1Router.vm.network "private_network", adapter: 4, auto_config: false, virtualbox__intnet: "vlan1"
    office1Router.vm.network "private_network", adapter: 5, auto_config: false, virtualbox__intnet: "vlan2"
    office1Router.vm.network "private_network", adapter: 6, auto_config: false, virtualbox__intnet: "vlan2"
    office1Router.vm.network "private_network", adapter: 8, ip: '192.168.56.20'
    office1Router.vm.hostname = "office1Router"
  end
  config.vm.define "testClient1" do |testClient1|
    testClient1.vm.box = "centos/7"
    testClient1.vm.box_version = "2004.01"
    testClient1.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
    testClient1.vm.network "private_network", adapter: 8, ip: '192.168.56.21'
    testClient1.vm.hostname = "testClient1"
  end
  config.vm.define "testServer1" do |testServer1|
    testServer1.vm.box = "centos/7"
    testServer1.vm.box_version = "2004.01"
    testServer1.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
    testServer1.vm.network "private_network", adapter: 8, ip: '192.168.56.22'
    testServer1.vm.hostname = "testServer1"
  end
  config.vm.define "testClient2" do |testClient2|
    testClient2.vm.box = "hashicorp/bionic64"
    testClient2.vm.box_version = "1.0.282"
    testClient2.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
    testClient2.vm.network "private_network", adapter: 8, ip: '192.168.56.31'
    testClient2.vm.hostname = "testClient2"
  end  
  config.vm.define "testServer2" do |testServer2|
    testServer2.vm.box = "hashicorp/bionic64"
    testServer2.vm.box_version = "1.0.282"
    testServer2.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
    testServer2.vm.network "private_network", adapter: 8, ip: '192.168.56.32'
    testServer2.vm.hostname = "testServer2"
  end
end
