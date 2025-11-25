Vagrant.configure("2") do |config|
  # Box base
  config.vm.box = "ubuntu/jammy64"

  config.vm.hostname = "LNXWORDPRESSAPP"
  

  # Rede pública (bridge) — substitua "enp1s0" pelo nome da interface correta do seu host
  config.vm.network "public_network", bridge: "enp1s0"

  # Pasta sincronizada (host ./scripts → guest /mnt/scripts)
  config.vm.synced_folder "./scripts", "/mnt/scripts"

  # Configurações do VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.name = "LNXWORDPRESSAPP"
    vb.memory = 1024
    vb.cpus = 2
  
  end
  
  config.vm.provision "shell", inline: <<-SHELL
  sudo -i
  apt install apache2 wget unzip vim -y
  systemctl start apache2
  systemctl enabled apache2
  mkdir -p /tmp/WEBAPP
  cd /tmp/WEBAPP
  wget https://www.tooplate.com/zip-templates/2089_meteor.zip
  unzip -o 2089_meteor.zip
  cp -r 2089_meteor/* /var/www/html/
  systemctl restart apache2
SHELL

end

