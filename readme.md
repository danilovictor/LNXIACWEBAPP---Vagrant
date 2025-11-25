# 🌐 Provisionamento Automático de Máquina Virtual para Servidor Web com Vagrant + Apache2
Deploy automatizado de template HTML (Tooplate) em Ubuntu Jammy

## 📘 Sobre o Projeto

Este repositório demonstra como criar um ambiente automatizado utilizando Vagrant + VirtualBox, instalando e configurando automaticamente o Apache2, além de fazer o deploy de um template HTML baixado do site Tooplate.


## 🧱 Estrutura do Projeto

📦 Projeto-Web-Vagrant
 ┣ 📂 scripts/        # Pasta sincronizada (opcional)
 ┣ 📄 Vagrantfile     # Arquivo principal
 ┗ 📄 README.md

## 🖥️ Requisitos

Antes de começar, instale:

**Vagrant** → https://www.vagrantup.com
**VirtualBox** → https://www.virtualbox.org

## ⚙️ Vagrantfile

Vagrant.configure("2") do |config|
   Box base
  config.vm.box = "ubuntu/jammy64"

  config.vm.hostname = "LNXWORDPRESSAPP"
  
   Rede pública (bridge) — substitua "enp1s0" pelo nome da interface correta do seu host
  config.vm.network "public_network", bridge: "enp1s0"

   Pasta sincronizada (host ./scripts → guest /mnt/scripts)
  config.vm.synced_folder "./scripts", "/mnt/scripts"

   Configurações do VirtualBox
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

## 🔍 Explicação do Provisionamento
✔ **Instalações realizadas automaticamente**

Apache2

wget

unzip

vim

## ✔ Operações realizadas

Download do template Meteor (Tooplate)

Extração e cópia dos arquivos para /var/www/html/

Inicialização e habilitação do Apache2

## ▶️ Como Usar
1️⃣ **Iniciar a máquina**

vagrant up

2️⃣ **Acessar via SSH**

vagrant ssh

3️⃣ **Parar a VM**

vagrant halt

4️⃣ **Resetar e recriar tudo**

vagrant destroy -f
vagrant up

## 🌍 **Acessando a Aplicação**

Dentro da VM:

ip a

Localize o IP da interface bridge e abra no navegador:

http://SEU_IP

Exemplo:

http://192.168.0.120

## 📌 Objetivos do Projeto

Infraestrutura como código

Ambientes replicáveis de desenvolvimento

Automatizar deploys básicos

Deploy Web APP

Criar base para pipelines CI/CD

## 🤝 Contribuição

Pull requests são bem-vindos!
Para mudanças significativas, abra uma issue primeiro para discussão.