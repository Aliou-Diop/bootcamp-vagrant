# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  config.vm.define "server" do |webserver|
    
    webserver.vm.box = "ubuntu/trusty64"

    webserver.vm.box_check_update = false

    webserver.vm.network "forwarded_port", guest: 80, host: 8082

    webserver.vm.network "private_network", type: "static", ip: "192.168.0.10"

    webserver.vm.synced_folder "./tomcatwebapps", "/opt/tomcat/webapps"

    webserver.vm.provider "virtualbox" do |vb|
   
      vb.gui = true
      vb.name = "webserver-tomcat"
      vb.memory = "1024"
    end

  end
end


Vagrant.configure("2") do |config|
  
  # Serveur BDD MySQL
  config.vm.define "server-db" do |dbserver|
    
    dbserver.vm.box = "ubuntu/trusty64"
    dbserver.vm.box_check_update = false
    dbserver.vm.network "private_network", type: "static", ip: "192.168.0.10"

    dbserver.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.name = "server-mysql"
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

  # Serveur Web Tomcat
  config.vm.define "server" do |webserver|
    webserver.vm.box = "ubuntu/trusty64"
    webserver.vm.box_check_update = false

    webserver.vm.network "forwarded_port", guest: 80, host: 8082
    webserver.vm.network "private_network", type: "static", ip: "192.168.0.12" # ⚠️ Change l'IP pour éviter un conflit avec "server-db"

    webserver.vm.synced_folder "./tomcatwebapps", "/opt/tomcat/webapps"

    webserver.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.name = "webserver-tomcat"
      vb.memory = "1024"
    end
  end

  # Serveur Web Preprod
  config.vm.define "preprodserver" do |preprodwebserver|
    
    preprodwebserver.vm.box = "bento/ubuntu-22-04"
    preprodwebserver.vm.box_check_update = false

    preprodwebserver.vm.network "forwarded_port", guest: 8080, host: 8083
    preprodwebserver.vm.network "private_network", type: "static", ip: "192.168.0.11"

    preprodwebserver.vm.synced_folder "./tomcatwebapps", "/opt/tomcat/webapps"
    preprodwebserver.vm.synced_folder "./tomcatconf", "/opt/tomcat/conf"

    preprodwebserver.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.name = "preprod-webserver"
      vb.memory = "1024"
    end
  end
end