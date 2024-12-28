CONFIG = File.expand_path("vagrant-config.rb")

require CONFIG

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  # Количество требуемых машин
  SERVERS = 2

  def create_host(config, hostname, ip)
    config.vm.define hostname do |host|
      host.vm.network "private_network", ip: ip
      host.vm.network "public_network", bridge: $BRIDGE
      host.vm.hostname = hostname
      host.vm.provision "shell", inline: "apt-get update && apt-get install -y python2-minimal"
      host.vm.provision "file", source: $SSH_PUBLIC_KEY_PATH, destination: "/tmp/ssh_key.pub"
      host.vm.provision "shell", inline: <<-SHELL 
        cat "/tmp/ssh_key.pub" >> /home/vagrant/.ssh/authorized_keys
      SHELL
      yield host if block_given?
    end
  end

  (1..SERVERS).each do |machine_id|
    create_host(config, "srv#{machine_id}", "192.168.56.#{200+machine_id}")
  end

end
