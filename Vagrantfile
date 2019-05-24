# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # complete reference: https://docs.vagrantup.com.
  config.vm.box = "ubuntu/bionic64"

  # disk size
  required_plugins = %w( vagrant-disksize )
  _retry = false
  required_plugins.each do |plugin|
    unless Vagrant.has_plugin? plugin
      system "vagrant plugin install #{plugin}"
      _retry=true
    end
  end
  config.disksize.size = '50GB'

  # expose vagarnt box port 80 via host machine port 8080
  # remove (or extend) the 'host_ip' setting to make access public
  config.vm.network "forwarded_port", guest: 80,   host: 8080, host_ip: "127.0.0.1"

  # shared folders
  config.vm.synced_folder ".", "/home/vagrant/GPS_dataviewer"

  # virtualbox settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192"
  end

  config.vm.provision "shell", inline: <<-SHELL
   apt-get update -qq
   apt-get install --yes   cpanminus                  \
                           libmariadbclient-dev       \
                           mariadb-server             \
                           mariadb-client
   cpanm inc::Module::Install                         \
         Catalyst::Authentication::Store::DBIx::Class \
         Catalyst::Plugin::Authentication             \
         Catalyst::Plugin::Session::State::Cookie     \
         Catalyst::Plugin::Session::Store::FastMmap   \
         Catalyst::View::TT                           \
         Log::Log4perl::Catalyst                      \
         Module::Install::Catalyst                    \
         DBD::mysql                                   \
         DBI                                          \
         File::ReadBackwards                          \
         JSON                                         \
         Moose                                        \
         MooseX::NonMoose                             \
         Spreadsheet::XLSX                            \
         Term::Size::Any                              \
         Text::CSV
   cd GPS_dataviewer
   sudo -u vagrant mkdir -p ./tmp/downloads
   sudo -u vagrant perl -w Makefile.PL
   sudo -u vagrant bash -c 'make && make test && make install'
   SHELL
end

