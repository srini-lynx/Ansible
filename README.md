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

Step by Step Procedure to Use Ansible Script 

#######################################################################

1> Initialize Vagrant File . 

2> Once Initialized , Copy the Vagrant Code above to the Vagrant File  Save & Quit

3> vagrant up 

4> Once you get the hadoop and ansible nodes are up and running check and verify the same 

5> vagrant status 

6> vagrant ssh ansible 

7> Once you are inside the Vagrant Ansible m/c 

8> git clone https://github.com/srini-lynx/Ansible.git 

9> After you Successfully cloned, use the hadoop-pseuodo.yml file by using command : ansible-playbook <filename>.yml

10> login to  hadoop node through Vagrant 

ex: vagrant ssh hadoop 

11> Once inside the hadoop node 

    $hadoop hdfs -format  (Format the Name node with HDFS Filesystem)
    $start-all.sh   (Start all the Hadoop Daemons  )
    $jps (Ensure All the Daemons are up and running , Resource manager,node manager,datanode ..etc)

########################################################################
