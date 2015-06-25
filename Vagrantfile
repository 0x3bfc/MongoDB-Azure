# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.boot_timeout = 1000

  common_azure = Proc.new do |azure, override|
        config.vm.box = 'azure'

        azure.mgmt_certificate = 'cert/cert.pem'
        azure.mgmt_endpoint = 'https://management.core.windows.net'
        azure.subscription_id = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX' # your subscription id
        azure.storage_acct_name = 'mulyvagrant'
        azure.vm_image = '5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-65-20150325'
        azure.vm_user = 'ahmed' # change to username on your local host
	azure.ssh_private_key_file = '/home/ahmed/.ssh/id_rsa'	# change the path of id_rsa to yours
	azure.ssh_certificate_file = '/home/ahmed/.ssh/ssh-cert.pem' # change the path of ssh-cer.pem to yours
        azure.vm_name = 'mongo-azure'
        azure.cloud_service_name = 'mongo-azure-tests' # same as vm_name. leave blank to auto-generate
        azure.deployment_name = 'mongo-azure-muly' # defaults to cloud_service_name
        azure.vm_location = 'West US' # e.g., West US
	azure.ssh_port = '22'
	azure.tcp_endpoints = '27017:27017, 7777:7777, 8888:8888'
  end

  config.vm.define 'master' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'mongo-master'
      azure.ssh_port = 2200
      azure.tcp_endpoints = '40000:40000, 7770:7770, 8880:8880, 40001:10100, 7771:10200, 8881:10300, 40002:10400, 7772:10500, 8882:10600'
    end
  end

  config.vm.define 'replica1' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'mongo-replica1'
      azure.ssh_port = 2201
      azure.tcp_endpoints = '40001:40001, 7771:7771, 8881:8881, 40000:20100, 7770:20200, 8880:20300, 40002:20400, 7772:20500, 8882:20600'
    end
  end

  config.vm.define 'replica2' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'mongo-replica2'
      azure.ssh_port = 2202
      azure.tcp_endpoints = '40002:40002, 7772:7772, 8882:8882, 40001:30100, 7771:30200, 8881:30300, 40000:30400, 7770:30500, 8880:30600'
    end
  end

end
