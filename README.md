# Vagrant development box for Swift

Starting with ubuntu/trusty64, this adds:
    * Swift


# Installation into your project

1. Copy `Vagrantfile` and `vm-provisioning` folder into your project.
2. Open `Vagrantfile` and change:
    - the IP address on `config.vm.network` if you need to.
    - the hostname (`config.vm.network`)
3. Update the swift_snapshot in `vm-provisioning\init.yml`
5. Add .vagrant to your project's `.gitignore` file.


## Running the VM

1. Install VitualBox, VirtualBox Guest Additions and Vagrant.

2. Run `vagrant up` from the command line.

3. Add hostname to `/etc/hosts`.
   
    - Use the IP address that's in your `Vagrantfile`.

       e.g

          192.168.99.2 swiftdev.localhost
