# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.define :local do |local|
    local.vm.box = "chef/centos-6.5"
    local.vm.network "private_network", ip: "192.168.33.40"
    local.cache.scope = :box if Vagrant.has_plugin? 'vagrant-cachier'
  end


  config.vm.define 'aws', autostart: false do |aws|
    aws.vm.box_url  = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
    aws.vm.box = "dummy"
    aws.vm.provider 'aws' do |aws, override|
      aws.access_key_id     = ENV['AWS_ACCESS_KEY_ID']
      aws.secret_access_key = ENV['AWS_SECRET_KEY']
      aws.keypair_name = "vagrant-test"

      aws.tags = { 'Name' => 'aws' }
      aws.instance_type = "t1.micro" # CPU:2ECU x1, Memory size:613MiB

      aws.ami = "ami-173fbf16" # "Amazon Linux 2013.03 minimal"
      aws.region = "ap-northeast-1"
      aws.availability_zone = "ap-northeast-1c"
      aws.subnet_id = ENV['AWS_SUBNET_ID']
      aws.security_groups = ENV['AWS_SG_GROUP']

      aws.block_device_mapping = [
        {
        # デバイス名
        'DeviceName' => "/dev/sda1",
        # 名称
        'VirtualName' => "aws",
        # ボリュームサイズ（GB単位）
        'Ebs.VolumeSize' => 8,
          'Ebs.DeleteOnTermination' => true
        }
      ]

      override.ssh.username = "ec2-user"
      override.ssh.private_key_path =  ENV['AWS_SSH_KEY_PATH']

      ## Use pty Vagrantでsshするのに必要？
      override.ssh.pty = true

    end
  end
end
