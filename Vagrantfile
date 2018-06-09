Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu-18.04-amd64"

  config.vm.hostname = "gitlab.example.com"

  config.vm.network "private_network", ip: "192.168.33.20"

  config.vm.provider "virtualbox" do |vb|
    vb.linked_clone = true
    vb.memory = 2048
    vb.cpus = 2
  end

  config.trigger.before :up do
    ldap_ca_cert_path = '../windows-domain-controller-vagrant/tmp/ExampleEnterpriseRootCA.der'
    run "sh -c 'mkdir -p tmp && cp #{ldap_ca_cert_path} tmp'" if File.file? ldap_ca_cert_path
  end

  config.vm.provision "shell", path: "provision.sh"
end
