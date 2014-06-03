vagrant-vcloud-box
==================

Ubuntu Desktop box with preinstalled Vagrant and vagrant-vcloud plugin
to have a working environment to connect to vCloud.

## Preparation

### SSH Keys

To clone private GitHub repos, you may place your SSH key here: 

```
resources/.ssh/id_rsa
resources/.ssh/id_rsa.pub
resources/.ssh/known_hosts
```

They will be copied into the box.

### Global Vagrantfile

Your connection data into your vCloud org or other global Vagrant
settings could be placed in the following file:

```
resources/Vagrantfile
```

This file will be copied into `~/.vagrant/Vagrantfile` in the guest VM.

This file may look like this one:

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-vcloud")
    # vCloud Director provider settings
    config.vm.provider :vcloud do |vcloud|
      vcloud.hostname = "https://yourvcloudhost"
      vcloud.username = "vagrant"
      vcloud.password = "XXXXXXX"

      vcloud.org_name = "XX"
      vcloud.vdc_name = "XX-ORG"

      vcloud.catalog_name = "Vagrant"

      vcloud.vdc_network_name = "XX-INTERNAL"

      vcloud.vdc_edge_gateway = "XX-EDGE"
      vcloud.vdc_edge_gateway_ip = "10.100.XX.X"
    end
  end

end
```