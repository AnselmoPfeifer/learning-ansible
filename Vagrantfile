VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |vconfig|
    vconfig.vm.box = "precise64"
    vconfig.vm.box_url = "http://files.vagrantup.com/precise64.box"

    vconfig.vm.define :site do |config|
        config.vm.provider :virtualbox do |v|
            #set memory to > 256M
            v.customize [ "modifyvm", :id, "--memory", "1100" ]
            v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
        end
        config.vm.host_name = "sitevagrant"

        config.vm.synced_folder "./", "/vagrant", :mount_options => ['dmode=777', 'fmode=666'] #, :nfs=>true
#        config.vm.network :private_network, ip: "10.10.10.10"

        #forward to port 8888
        config.vm.network "forwarded_port", guest: 80, host: 8888

        config.vm.provision :shell, :path => "ansible/provision.sh"
    end
end
