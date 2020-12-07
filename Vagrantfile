# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.synced_folder "./k8s", "/k8s"

  config.vm.network :private_network, ip: "192.168.33.100"
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = 4096
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Trust your enterprise certificates
    SHARE=/vagrant/ca-trust
    CERTS=/usr/local/share/ca-certificates

    if [ -d $SHARE ]; then
      # http://manpages.ubuntu.com/manpages/focal/man8/update-ca-certificates.8.html
      cp $SHARE/*.crt $CERTS
      update-ca-certificates

      # https://snapcraft.io/docs/system-options#heading--store-certs
      shopt -s nullglob
      FILES=($CERTS/*.crt)
      for i in ${!FILES[@]}; do
        FILENAME=${FILES[$i]}
        CERTNAME="custom-$i"
        echo "Store certs in snap: $(basename ${FILENAME})"
        snap set system store-certs."${CERTNAME}"="$(cat ${FILENAME})"
      done
    fi
    
  SHELL

end
