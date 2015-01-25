# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.define 'test', autostart: false do |test|
    test.vm.box_url  = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
    test.vm.box = "dummy"
    test.vm.provider 'aws' do |aws, override|
      aws.access_key_id     = ENV['AWS_ACCESS_KEY_ID']
      aws.secret_access_key = ENV['AWS_SECRET_KEY']
      aws.keypair_name = "vagrant-test"

      aws.tags = { 'Name' => 'test' }
      aws.instance_type = "t1.micro" # CPU:2ECU x1, Memory size:613MiB

      aws.ami = "ami-173fbf16" # "Amazon Linux 2013.03 minimal"
      aws.region = "ap-northeast-1"
      aws.availability_zone = "ap-northeast-1c"
      aws.subnet_id = ENV['AWS_SUBNET_ID']
      aws.security_groups = [ 'vagrant' ]

      aws.block_device_mapping = [
        {
        # デバイス名
        'DeviceName' => "/dev/sda1",
        # 名称
        'VirtualName' => "test",
        # ボリュームサイズ（GB単位）
        'Ebs.VolumeSize' => 8,
          'Ebs.DeleteOnTermination' => true
        }
      ]

      override.ssh.username = "ec2-user"
      override.ssh.private_key_path = "./vagrant-test.pem"

    end
  end
end
