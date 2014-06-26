VAGRANTFILE_API_VERSION = "2"

Vagrant::Config.run(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-amd64-vagrant-disk1.box"


  config.vm.network :public_network

  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  #
  config.vm.provision :shell, :path => "install-rvm.sh",  :args => "stable"
  config.vm.provision :shell, :path => "install-ruby.sh", :args => "2.0.0"
  config.vm.provision :shell, :path => "install-mongo.sh"

  config.vm.provision :shell, :path => "nvm-provision.sh"

  if Dir.glob("#{File.dirname(__FILE__)}/.vagrant/machines/default/*/id").empty?
     pkg_cmd = "apt-get update -qq; apt-get install -q -y build-essential git " \
        "autoconf autoconf-archive gnu-standards help2man texinfo; "
    pkg_cmd << "apt-get install -q -y erlang-base-hipe erlang-dev " \
        "erlang-manpages erlang-eunit erlang-nox erlang-xmerl erlang-inets; "
    pkg_cmd << "apt-get install -q -y libmozjs185-dev libicu-dev " \
        "curl libcurl4-gnutls-dev libtool; "
    pkg_cmd << "apt-get install -q -y help2man texinfo python-sphinx python-pip; " \
        "pip install -U pygments; "

    pkg_cmd << "apt-get install couchdb; "

    config.vm.provision :shell, :inline => pkg_cmd
  end
  
end
