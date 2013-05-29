# encoding: utf-8

Vagrant.configure("2") do |config|

  # 
  # BOX
  # 

  # *** Chef 11.4.0 ***
  # system_chef_solo: '/opt/chef/bin/chef-solo'
  config.vm.box = "omnibus"
  config.vm.box_url = "https://s3.amazonaws.com/gsc-vagrant-boxes/ubuntu-12.04-omnibus-chef.box"
  

  # How to upgrade Chef on vagrant boxes
  # http://stackoverflow.com/questions/11325479/how-to-control-the-version-of-chef-that-vagrant-uses-to-provision-vms
  
  # *** Chef 10.14.2 *** 
  # issues with some dependecies - need specify version 0.1.0 in Cheffile until upgrade to Chef 11
  # http://community.opscode.com/cookbooks/ark/comments 

  # Vagrant Chef install path
  # system_chef_solo: /opt/vagrant_ruby/bin/chef-solo
  # 
  # Origignal Chef 11.4 install path
  # system_chef_solo: /opt/chef/bin/chef-solo 

  # config.vm.box     = 'precise32'
  # config.vm.box_url = 'http://files.vagrantup.com/precise32.box'

  # *** Chef 10.14.2 ***
  # system_chef_solo: /opt/vagrant_ruby/bin/chef-solo
  # config.vm.box     = 'precise64'
  # config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # 
  # NETWORK  
  #

  config.vm.network :private_network, ip: '10.255.255.10'
  config.ssh.forward_agent = true

  # NFS - speedup file synchronization vs standard mode 
  # config.vm.synced_folder "~/code", "/home/vagrant/code", :nfs => true

  # Webrick
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  # MySQL
  config.vm.network :forwarded_port, guest: 3306, host: 3306

  # config.vm.network :forwarded_port, guest: 4000, host: 4000
  # config.vm.network :forwarded_port, guest: 4567, host: 4567
  # PostgreSQL
  # config.vm.network :forwarded_port, guest: 5432, host: 5432
  # config.vm.network :forwarded_port, guest: 9292, host: 9292

  # VM Box memory customization (default value may vary - depend on box type)
  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', 1024]
  end

  # 
  # CHEF
  # 

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe 'apt'
    chef.add_recipe 'git'
    # chef.add_recipe 'mysql::server'

    chef.add_recipe 'rvm::vagrant'
    chef.add_recipe 'rvm::system'

    # chef.add_recipe 'redis::install_from_package'
    # chef.add_recipe 'oh_my_zsh'
    chef.add_recipe 'locale'

    chef.json = {
      rvm: {
        vagrant: {
          # default path in new vagrant boxes is '/opt/vagrant_ruby/bin/chef-solo'
          # see cookbokes/rvm/attributes/vargant.rb
          # but third-party boxes uses different path to chef, 
          # so we need provide correct path specific to used box
          system_chef_solo: '/opt/chef/bin/chef-solo'
        },
        default_ruby: 'ruby-1.9.3-p429'
      },      
      :mysql => {
        :server_root_password   => "password",
        :server_repl_password   => "password",
        :server_debian_password => "password",
        :service_name           => "mysql",
        :basedir                => "/usr",
        :data_dir               => "/var/lib/mysql",
        :root_group             => "root",
        :mysqladmin_bin         => "/usr/bin/mysqladmin",
        :mysql_bin              => "/usr/bin/mysql",
        :conf_dir               => "/etc/mysql",
        :confd_dir              => "/etc/mysql/conf.d",
        :socket                 => "/var/run/mysqld/mysqld.sock",
        :pid_file               => "/var/run/mysqld/mysqld.pid",
        :grants_path            => "/etc/mysql/grants.sql"
      },
      'oh_my_zsh' => {
        'users' => [{
          :login => 'vagrant',
          :theme => 'mortalscumbag',
          :plugins => ['gem', 'git', 'rails3', 'redis-cli', 'ruby', 'heroku', 'rake', 'rvm', 'capistrano']
        }]
      }
    }
  end
end