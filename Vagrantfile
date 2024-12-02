# Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos9s"

  config.vm.network "forwarded_port", guest: 80, host: 8888

  config.vm.provision "shell", inline: <<-SHELL
    # Install Nginx
    yum install -y epel-release
    yum install -y nginx

    # Disable SELinux and confirm
    setenforce 0
    sed -i 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config
    cat /etc/selinux/config

    # Start and enable Nginx
    systemctl start nginx
    systemctl enable nginx

    # Disable firewalld
    systemctl stop firewalld
    systemctl disable firewalld
  SHELL

  config.vm.synced_folder "/www-content", "/usr/share/nginx/html"
end

