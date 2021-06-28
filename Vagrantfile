# -*- mode: ruby -*-
# vi: set ft=ruby :

#global script
$global = <<SCRIPT

echo "Start Provisioning"
sudo -S apt update -y
sudo rm -rf /usr/bin/pip
sudo rm -rf /usr/local/bin/pip
sudo rm -rf /usr/bin/python
sudo rm -rf /usr/local/bin/python
sudo DEBIAN_FRONTEND=noninteractive apt install -y python3 python3-pip ethtool build-essential linux-headers-$(uname -r) dkms libssl-dev libffi-dev python-dev unzip libmysqlclient-dev  python3-mysqldb python3.8-distutils
sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 10
sudo update-alternatives --install /usr/local/bin/pip pip /usr/bin/pip3 10
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
echo "Finish Provisioning"

SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.5.0"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # VB Guest Additions configuration:
  #
  if Vagrant.has_plugin?('vagrant-vbguest')
    config.vbguest.auto_reboot = true
    # Do **NOT** force update if image already has pre-installed vbguest
    # - https://forums.virtualbox.org/viewtopic.php?f=7&t=86819
    # - https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1783267
    # - https://stackoverflow.com/questions/37556968/vagrant-disable-guest-additions
    #
    config.vbguest.auto_update = false
  else
    puts 'INFO: vagrant plugin is missing. Install it by running:'
    puts 'INFO: $ vagrant plugin install vagrant-vbguest'
    exit
  end

  if Vagrant.has_plugin?('vagrant-disksize')
    config.disksize.size = '20GB'
  else
    puts 'INFO: vagrant plugin is missing. Install it by running:'
    puts 'INFO: $ vagrant plugin install vagrant-disksize'
    exit
  end

  config.vm.box = "ubuntu/focal64"
  # config.vm.box = "rogal/cloud9"
  # config.vm.box_version = "0.0.1"
  # config.vm.synced_folder ".", "/vagrant", type: 'nfs'

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize [
      "modifyvm", :id,
      "--memory", "2048",
    #   # set available CPU's count
      "--cpus", 1,
    #   "--ioapic", "off",
    #   "--audio", "none",
    #   "--uartmode1", "disconnected",
    #   "--uart1", "0x3F8", "4",
    #   "--uartmode1", "file", File::NULL,
    #   "--cableconnected1", "on"
    ]
  end

  # config.disksize.size = '20GB'
  # config.vm.network :forwarded_port, guest: 30000, host: 30000

  # config.ssh.insert_key = true
  # config.ssh.username = 'vagrant'
  # config.ssh.private_key_path = [ 'vagrant_key' ]
  # config.vm.provision "file", source: "keys/public", destination: "~/.ssh/authorized_keys"

  config.vm.define :basebox, autostart: false do |config|
    config.vm.provision "shell", privileged: true, inline: $global
    config.vm.boot_timeout = 600

    config.vbguest.auto_update = false
    config.vm.provision :ansible_local, playbook: "playbook-base.yml"
  end

  config.vm.define :cloudbox, primary: true do |config|
    config.vm.network :private_network, ip: "192.168.3.5"
    config.vm.box = "rogal/cloud-dev-box"
    config.vm.box_version = "0.0.1"
    config.vm.provision :ansible_local, playbook: "playbook.yml"
  end

  ## Utils
  ## Resize VM disk
  # VBoxManage clonemedium "source.vmdk" "cloned.vdi" --format vdi
  # VBoxManage modifymedium "cloned.vdi" --resize 51200
  # VBoxManage clonemedium "cloned.vdi" "resized.vmdk" --format vmdk

  ## mount vagrant folder
  # /opt/VBoxGuestAdditions-6.0.10/other/mount.vboxsf -o uid=1000,gid=1000 vagrant /vagrant

end