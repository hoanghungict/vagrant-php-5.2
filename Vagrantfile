Vagrant.configure("2") do |config|

  config.vm.box = "tierra/wordpress-php52"

  forward_port = ->(guest, host = guest) do
    config.vm.network :forwarded_port,
      guest: guest,
      host: host,
      auto_correct: true
  end

  # Sync between the web root of the VM and the 'sites' directory
  config.vm.synced_folder "/var/www", "/var/www", :mount_options => ["dmode=777","fmode=666"]

  forward_port[1080]      # mailcatcher
  forward_port[3306]      # mysql
  forward_port[80, 8080]  # nginx/apache

  config.ssh.username = 'vagrant'
  config.ssh.password = 'vagrant'
  config.ssh.insert_key = false

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file = "default.pp"
  end

  config.vm.network :private_network, ip: "44.44.44.10"
end
