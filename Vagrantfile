Vagrant.configure('2') do |config|
  config.vm.define "pravega_standalone" do |pravega|

    #pravega.vm.provision "shell", inline: "apt-get update", privileged: true
    #pravega.vm.provision "shell", inline: "apt-get -y install build-essential linux-headers-`uname -r`", privileged: true
    #pravega.vm.provision "shell", inline: "sudo -E apt-get -y install git zip", privileged: true
    #pravega.vm.provision "file", source: "vagrant", destination: "vagrant"
    #pravega.vm.provision "shell", inline: "chmod 755 vagrant/install-jdk.sh", privileged: true
    #pravega.vm.provision "shell", inline: "vagrant/install-jdk.sh", privileged: true
    pravega.vm.provider :virtualbox do |v, override|

      override.vm.box = 'ubuntu/trusty64'
      override.vm.network :private_network, ip: '192.168.50.14', id: :local
      override.vm.network :public_network
      v.memory = 6144
      v.cpus = 2
    end

    config.vm.provision "shell", inline: <<-SHELL
      add-apt-repository ppa:openjdk-r/ppa -y
      apt-get update
      apt-get upgrade -y
      echo "Install common tools"
      apt-get install -y nano git
      echo "Install Java and Maven"
      apt-get install -y openjdk-8-jdk openjdk-8-jdk-headless maven
      apt-get remove -y openjdk-7-jre openjdk-7-jre-headless
      git clone https://github.com/pravega/pravega.git
      cd pravega
      ./gradlew distribution
      
    SHELL
  end
end