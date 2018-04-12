
Vagrant.configure("2") do |config|

config.vm.provider "virtualbox" do |v|
  v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end

$scriptNode2 = <<-SCRIPT
echo Inizializzazione nodo2
sudo yum -y update
echo Installo java
sudo yum -y install java
echo Installo git
sudo yum -y install git
echo Installo jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum -y install jenkins
sudo service jenkins start
SCRIPT

$scriptNode1 = <<-SCRIPT
echo Inizializzazione nodo1
sudo yum -y update
echo Installo ansible
sudo yum -y install ansible
SCRIPT

config.vm.define "node1" do |node1|
  node1.vm.box = "bento/centos-7.4"
  node1.vm.network "private_network", ip: "192.168.0.101"
  node1.vm.hostname = "node1"
  node1.vm.provision "shell", inline: $scriptNode1
end
config.vm.define "node2" do |node2|
  node2.vm.box = "bento/centos-7.4"
  node2.vm.network "private_network", ip: "192.168.0.102"
  node2.vm.hostname = "node2"
  node2.vm.provision "shell", inline: $scriptNode2
  node2.vm.network "forwarded_port", guest: 8080, host: 9999
end

   
end
