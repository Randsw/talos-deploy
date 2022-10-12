$k8s_master_num = 3
$k8s_worker_num = 3

Vagrant.configure("2") do |config|
  (1..($k8s_master_num + $k8s_worker_num)).each do |i|
    if i < $k8s_master_num + 1
      config.vm.define "control-plane-node-#{i}" do |node|
        node.vm.provider :libvirt do |domain| 4
          domain.cpus = 2
          domain.memory = 2048
          domain.serial :type => "file", :source => {:path => "/tmp/control-plane-node-#{i}.log"}
          domain.storage :file, :device => :cdrom, :path => "/home/rand/work/k8s/talos/talos-amd64.iso"
          domain.storage :file, :size => '4G', :type => 'raw'
          domain.boot 'hd'
          domain.boot 'cdrom'
        end
      end
    end
    if i > $k8s_master_num
      config.vm.define "worker-node-#{i-$k8s_worker_num}" do |node|
      node.vm.provider :libvirt do |domain|
          domain.cpus = 2
          domain.memory = 2048
          domain.serial :type => "file", :source => {:path => "/tmp/worker-node-#{i-$k8s_worker_num}.log"}
          domain.storage :file, :device => :cdrom, :path => "/home/rand/work/k8s/talos/talos-amd64.iso"
          domain.storage :file, :size => '4G', :type => 'raw'
          domain.boot 'hd'
          domain.boot 'cdrom'
        end
      end
    end
  end
end