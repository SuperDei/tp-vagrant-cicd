Vagrant.configure("2") do |config|
  # 1. On choisit une image Ubuntu légère (standard du web)
  config.vm.box = "ubuntu/focal64"

  # 2. On configure le réseau
  # On dit que le port 80 de la VM (site web) est accessible sur le port 8080 de ton PC
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 81, host: 8081
  
  # On donne une IP privée à la machine pour lui parler
  config.vm.network "private_network", ip: "192.168.56.10"

  # 3. Configuration de base (RAM/CPU)
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024" # 1 Go de RAM suffit
    vb.cpus = 1
    vb.name = "Serveur-Production"
  end

  # 4. Installation automatique de Nginx (Serveur Web) au démarrage
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y nginx git
    # On s'assure que le service tourne
    systemctl enable nginx
    systemctl start nginx
    # On donne les droits pour modifier le dossier web plus tard
    chown -R vagrant:vagrant /var/www/html
  SHELL
end