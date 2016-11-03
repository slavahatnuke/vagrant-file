VAGRANTFILE_API_VERSION = "2"

name = "project-name"
memory = "512"
cpu="2"
type="nfs" # options: "", "nfs"
ip = "192.168.10.20"
home = "/home/vagrant/project"
sync= "."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Base box
  config.vm.box = "ubuntu/trusty64"

  if type
    config.vm.synced_folder sync, home, type: type
  else
    config.vm.synced_folder sync, home
  end

  config.vm.network :private_network, ip: ip

  config.vm.provider "virtualbox" do |v|
    v.name = name
    v.customize ["modifyvm", :id, "--memory", memory]
    v.customize ["modifyvm", :id, "--cpus", cpu]
    v.customize ["modifyvm", :id, "--vram", "8"]
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  #PROVISION (shell)

  ##update
  config.vm.provision "shell", inline: "sudo apt-get -y update"

  ##curl
  config.vm.provision "shell", inline: "which curl || sudo apt-get install -y curl"

  ##git
  config.vm.provision "shell", inline: "which git || sudo apt-get install -y git"

  ##bash-completion
  config.vm.provision "shell", inline: "sudo dpkg -l | grep bash-completion || ( sudo apt-get install -y bash-completion )"

end