# chef-provision-memo

## chefdkのインストール

## chef-provisioning-sshのインストール

```
$chef gem install chef-provisioning-ssh
```

## 実行まで

リポジトリ作成
```
$chef generate repo chef-repo
$cd chef-repo
```

knife.rbの編集
```
$mkdir .chef
$echo local_mode true > .chef/knife.rb
```

tesh_ssh.rbの作成
```
require 'chef/provisioning/ssh_driver'

with_driver 'ssh'

machine "test" do
  machine_options :transport_options => {
    :ip_address => '192.168.0.2',
    :username => 'vagrant',
    :ssh_options => {
      :password => 'vagrant'
    }
  }
  recipe 'test'
  converge true
end
```

実行
```
chef-client -z test_ssh.rb --chef-zero-port 8899
```
