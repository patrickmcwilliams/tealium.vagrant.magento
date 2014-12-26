# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = 'precise64'

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # These ports are used to avoid conflicts with local services.
  config.vm.network :forwarded_port, host: 1080, guest: 80
  config.vm.network :forwarded_port, host: 13306, guest: 3306


  # This is to ensure Magento can write it's generated data to our media and var directories.
  config.vm.synced_folder "magento", "/vagrant",
    owner: "www-data", group: "vagrant",
    create: true,
    mount_options: ['dmode=777','fmode=777']

  config.vm.provision :chef_solo do |chef|
    # Chef Logging
    #chef.log_level = :debug

    chef.json = { 
      'vagrant_magento' => {
        'phpinfo_enabled' => true,
        'mage_check_enabled' => true,
        'sample_data' => { 
          'install' => true 
        },
        'config' => { 
          'install' => true 
        }
      }
    }
    chef.cookbooks_path = 'deploy_support/chef/cookbooks'
    chef.roles_path = 'deploy_support/chef/roles'
    chef.add_role 'magento_dev'
  end
end
