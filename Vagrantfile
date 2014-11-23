# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
vconfig = YAML::load_file("config.yml")

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu_aws"
  config.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
  config.vm.synced_folder "./vagrant_root/", "/vagrant", id: "vagrant-root"
  config.vm.provider :aws do |aws, override|
    aws.keypair_name = "development"
    aws.secret_access_key = vconfig['aws']['secret_access_key']
    aws.access_key_id = vconfig['aws']['access_key_id']
    override.ssh.private_key_path = "~/.ssh/development.pem"
    aws.instance_type = "t2.micro"
    aws.security_groups = "development"
    aws.ami = "ami-8827efe0"
    override.ssh.username = "ubuntu"
    aws.tags = {
      'Name' => 'Web App',
     }
  end

#  config.vm.provision :puppet do |puppet|
#    puppet.manifests_path = "puppet/manifests"
#    puppet.manifest_file  = "init.pp"
#    puppet.options = ["--fileserverconfig=/vagrant/puppet/fileserver.conf"]
#  end
end
