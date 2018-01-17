BOX_IMAGE = "centos/7"

Vagrant.configure("2") do |config|
  config.vm.define "jenkins" do |subconfig|
	subconfig.vm.box = BOX_IMAGE
	subconfig.vm.hostname = "jenkins"
	subconfig.vm.network :private_network, ip: "10.0.0.10"
	subconfig.vm.provision "shell", inline: <<-SHELL
		sudo yum install java wget git -y 
		sudo yum install java-1.8.0-openjdk-devel -y
		sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
		sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
		sudo yum install jenkins -y
		sudo service jenkins start
		curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
		sudo yum install -y nodejs
	  SHELL
  end
end
