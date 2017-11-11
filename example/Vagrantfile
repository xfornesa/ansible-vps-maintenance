Vagrant.configure("2") do |config|

  config.vm.define 'web01' do |config|
    config.vm.box = 'ubuntu/xenial64'
    config.vm.hostname = 'web01'
    config.ssh.forward_agent = true
    config.vm.network :forwarded_port, guest: 22, host: 2230, id: "ssh", auto_correct: false

    config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -q -y python
    SHELL
  end
end
