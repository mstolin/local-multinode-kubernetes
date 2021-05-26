NUMBER_OF_WORKER = 2
NUMBER_OF_NODES = NUMBER_OF_WORKER + 1
NODES = [
    { :name => "control-plane", :ip => "192.168.50.10" },
    { :name => "worker-1", :ip => "192.168.50.11" },
    { :name => "worker-2", :ip => "192.168.50.12" }
]

VM_IMAGE = "ubuntu/bionic64"
VM_MEMORY = 2048
VM_CPU = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |vbox|
        vbox.memory = VM_MEMORY
        vbox.cpus = VM_CPU
    end

    NODES.each_index do |node_idx|
        node = NODES[node_idx]

        config.vm.define node[:name] do |machine|
            machine.vm.box = VM_IMAGE
            machine.vm.network "private_network", ip: node[:ip]
            machine.vm.hostname = node[:name]

            #if node_idx == NUMBER_OF_NODES - 1
                #machine.vm.provision "ansible" do |ansible|
                    #ansible.groups = {
                    #    "control" => ["control-plane"],
                    #    "worker" => ["worker-1", "worker-2"],#["worker-[1:#{NUMBER_OF_WORKER}]"]
                    #    "all_groups:children" => ["control", "worker"]
                    #}
                    #ansible.host_vars = {
                    #    "control-plane" => {
                    #        "ansible_host" => "192.168.80.10"
                    #    },
                    #    "worker-1" => {
                    #        "ansible_host" => "192.168.80.11"
                    #    },
                    #    "worker-2" => {
                    #        "ansible_host" => "192.168.80.12"
                    #    }
                    #}
                    #ansible.inventory_path = "hosts.dev"
                    #ansible.config_file = "ansible.dev.cfg"
                    #ansible.playbook = "site.yaml"
                    #ansible.limit = ["all", "control", "worker"]
                #end
            #end
        end
    end
end
