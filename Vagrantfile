# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |c|
  c.vm.define "swiftdev", primary: true do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.network "private_network", ip: "192.168.99.202"

    # Set hostname
    config.vm.hostname = "swiftdev.localhost"

    # Prevent Vagrant 1.7 from asking for the vagrant user's password
    config.ssh.insert_key = false

    # config.vm.provider "virtualbox" do |vb|
    #   vb.customize ["modifyvm", :id, "--memory", "1024"]
    # end

    # Install ansible on guest
    config.vm.provision :shell,
      :keep_color => true,
      :inline => <<SCRIPT
        if [ $(dpkg-query -W -f='${Status}' ansible 2>/dev/null | grep -c "ok installed") -eq 0 ];
        then
            export DEBIAN_FRONTEND=noninteractive
            
            echo "Add Ansible repository"
            apt-add-repository ppa:ansible/ansible &> /dev/null || exit 1
            apt-get update -qq

            echo "Installing Ansible"
            apt-get install -qq ansible &> /dev/null || exit 1

            echo "Runing apt-get upgrade"
            apt-get update -qq &> /dev/null || exit 1
            apt-get upgrade -y &> /dev/null || exit 1
        fi


        echo "Running Ansible playbook"
        export PYTHONUNBUFFERED=1
        export ANSIBLE_FORCE_COLOR=1
        su vagrant -c "ansible-playbook -i 127.0.0.1, --connection=local /vagrant/vm-provisioning/init.yml"

SCRIPT

  
    # config.vm.provision "ansible" do |ansible|
    #   ansible.playbook = "vm-provisioning/init.yml"
    # end
  
  end
end
