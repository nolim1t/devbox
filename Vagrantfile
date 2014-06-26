VAGRANTFILE_API_VERSION = "2"

Vagrant::Config.run(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"


  config.vm.network :public_network, bridge: 'en0: Wi-Fi (AirPort)'

  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  #
  config.vm.provision :shell, :path => "install-rvm.sh",  :args => "stable"
  config.vm.provision :shell, :path => "install-ruby.sh", :args => "2.0.0"
  config.vm.provision :shell, :path => "install-mongo.sh"

  config.vm.provision :shell, :path => "nvm-provision.sh"

  if Dir.glob("#{File.dirname(__FILE__)}/.vagrant/machines/default/*/id").empty?
     pkg_cmd = "sudo apt-get update -qq; sudo apt-get install -q -y build-essential git " \
        "autoconf autoconf-archive gnu-standards help2man texinfo; "
    pkg_cmd << "sudo apt-get install -q -y erlang-base-hipe erlang-dev " \
        "erlang-manpages erlang-eunit erlang-nox erlang-xmerl erlang-inets; "
    pkg_cmd << "sudo apt-get install -q -y libmozjs185-dev libicu-dev " \
        "curl libcurl4-gnutls-dev libtool; "
    pkg_cmd << "sudo apt-get install -q -y help2man texinfo python-sphinx python-pip; " \
        "sudo pip install -U pygments; "

    pkg_cmd << "sudo apt-get install couchdb"

    config.vm.provision :shell, :inline => pkg_cmd
  end
  
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "512"]
  end
end
