UBUNTU_IMAGE = "ubuntu/bionic64"
NUMBER_OF_WORKER = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |vbox|
        vbox.memory = 2048
        vbox.cpus = 2
    end

    config.vm.define "k8s-control-plane" do |manager|
        CONTROL_PLANE_IP = "192.168.80.10"

        manager.vm.box = UBUNTU_IMAGE
        manager.vm.network "private_network", ip: CONTROL_PLANE_IP
        manager.vm.hostname = "control-plane"
    end

    (1..NUMBER_OF_WORKER).each do |i|
        config.vm.define "k8s-worker-#{i}" do |worker|
            WORKER_IP = "192.168.80.#{i + 10}"

            worker.vm.box = UBUNTU_IMAGE
            worker.vm.network "private_network", ip: WORKER_IP
            worker.vm.hostname = "worker-#{i}"
        end
    end
end
