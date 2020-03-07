Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "private_network", ip: '10.19.90.90'
  config.vm.define "blog" do |web|
    web.vm.provider :virtualbox do |vb|
      vb.name = "blog"
    end
  end
end
