HOSTNAME = "kops"
MEMORY = 8192 
CPUS = 2
DISK_SIZE = 70
INTERFACE = "wlxf4f26d0de085"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = HOSTNAME
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", type: "rsync"
  config.vm.network "public_network", ip: "192.168.1.10", bridge: "#{INTERFACE}"
  config.vm.network "forwarded_port", guest: 80, host: 8060 # Horizon
  config.vm.network "forwarded_port", guest: 3000, host: 3000 # Gitea
  config.vm.network "forwarded_port", guest: 5000, host: 5000 # Authentication
  config.vm.network "forwarded_port", guest: 8080, host: 8080 # Jenkins

  # Resize disk
  config.vm.disk :disk, size: "#{DISK_SIZE}GB", primary: true 

  config.vm.provider "virtualbox" do |vb|
    vb.memory = MEMORY
    vb.cpus = CPUS 
   end

  # Provisioning with ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
  end

  # Enable vagrant cachier plugin if it's already installed 
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

end
