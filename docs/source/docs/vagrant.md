# Vagrant
## Access vagrant from outsite
http://stackoverflow.com/questions/33358414/accessing-ngrok-web-interface-on-a-vagrant-box
ngrok http -host-header=rewrite mydomain.com:80

## package centos 7 box
config.ssh.insert_key = false

### add key
```
wget https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O .ssh/authorized_keys
chmod 700 .ssh
chmod 600 .ssh/authorized_keys
chown -R vagrant:vagrant .ssh
```

## Box export
VBoxManage list vms
vagrant package --base api_1537426240111_15426 --output ~/Documents/server/api-65.box
