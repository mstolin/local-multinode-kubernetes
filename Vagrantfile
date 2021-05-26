UBUNTU_IMAGE = "ubuntu/bionic64"
NUMBER_OF_NODES = 3

NODES = [
    { :name => "control-plane", :ip => "192.168.80.10" },
    { :name => "worker-1", :ip => "192.168.80.11" },
    { :name => "worker-2", :ip => "192.168.80.12" }
]

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |vbox|
        vbox.memory = 2048
        vbox.cpus = 2
    end

    NODES.each_index do |node_idx|
        node = NODES[node_idx]

        config.vm.define node[:name] do |machine|
            machine.vm.box = UBUNTU_IMAGE
            machine.vm.network "private_network", ip: node[:ip]
            machine.vm.hostname = node[:name]

            if node_idx == NUMBER_OF_NODES - 1
                machine.vm.provision "ansible" do |ansible|
                    ansible.inventory_path = "hosts.dev"
                    ansible.config_file = "ansible.dev.cfg"
                    ansible.playbook = "site.yaml"
                    ansible.limit = ["all", "control", "worker"]
                end
            end
        end
    end
end