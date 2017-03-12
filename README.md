# Ansible
Ansible Scripts
For Hadoop Pseuodo Cluster . It contains Ansible Code to Configure  Hadoop cluster right from Scratch by downloading the content from apache
hadoop.org , the binary tar ball. 

Once Ansible Script Ran Successfully , Need to Execute below commands .

$hadooop hdfs -format 
$start-all.sh 

Then Run the jps command and ensure all the hadoop daemons are running .



######################Below is the Vagrant File which needs to be provisioned first .

$ cat Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

###################Configuration for Ansible-Node

  config.vm.define "ansible" do |ansible|
     ansible.vm.box = "bento/ubuntu-16.04"
     ansible.vm.box_check_update = false
     ansible.vm.hostname = "ansible-node"
     ansible.vm.network "private_network", ip: "192.168.33.10"
     ansible.vm.provision "shell", inline: <<-SHELL
       sudo apt-get update
       sudo apt-get install ansible -y
     SHELL


end

###### Configuration For Hadoop-pseuodo node

   config.vm.define "hadoop" do |hadoop|
     hadoop.vm.box= "bento/ubuntu-16.04"
     hadoop.vm.box_check_update = false
     hadoop.vm.hostname = "hadoop-pseuodo"
     hadoop.vm.network "private_network", ip: "192.168.33.20"
     hadoop.vm.provision "shell" , inline: <<-SHELL
       sudo apt-get update
       sudo apt-get install openjdk-8-jdk -y
     SHELL

   end

#######################################################################

Once the Provision is over .

vagrant ssh ansible 

from Ansible node , clone the git repository 

and start using the Ansible script as stated earlier 


