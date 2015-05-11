Vagrant.configure("2") do |config|
  config.vm.define 'ubuntu' do |node|
    node.vm.box      = 'ubuntu/trusty64'
    node.vm.hostname = 'vagrant-ubuntu'

    node.ssh.insert_key = false 
    node.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'
    node.ssh.forward_agent = true
    node.vm.network :private_network, ip: '192.168.33.16'
    # mosh using port
    for i in 60000..60010 #official 60000..61000
      node.vm.network :forwarded_port, guest: i, host: i, protocol: 'udp'
    end
    node.vm.network :forwarded_port, guest: 3000, host: 3000
    node.vm.synced_folder 'synced_folder',
                          '/home/vagrant/synced_folder',
                          type:'nfs',
                          create:true 

    node.vm.provider :virtualbox do |vb|
      vb.customize ['modifyvm', :id, '--memory', '2048', '--cpus', '2', '--ioapic', 'on']
    end
  end
end
