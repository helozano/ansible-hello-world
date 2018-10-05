# ansible-hello-world

## vagrant servers

### create and run Vagrant VM

    # create the Vagrantfile
    vagrant init ubuntu/trusty64
    # start vagrant servers
    vagrant up

Eventually, add port mapping in your vagrantfile and run `vagrant reload`

### get the ssh config for to connecto to the VM
    vagrant ssh-config

### destroy image
    vagrant destroy [--force]

### ssh to vagrant
    vagrant ssh
    # or
    ssh vagrant@127.0.0.1 -p 2222 -i .vagrant/machines/default/virtualbox/private_key


## nginx

### create TLS certificate for the https
    openssl req -x509 -nodes -days 3650 -newkey rsa:2048 \
      -subj /CN=localhost \
      -keyout nginx/nginx.key -out nginx/nginx.crt

## ansible

### intall ansible

    sudo pip install ansible

### ping a host or a group

    ansible testserver -m ping
    ansible webservers -m ping
    ansible all -m ping
    ansible '*' -m ping

### ansible modules

    # command module
    ansible testserver [-m command] -a uptime
    
    # apt module as root
    ansible testserver -b -m apt -a name=nginx
    
    # service module as root
    ansible testserver -b -m service -a "name=nginx state=restarted"
    

### restart nginx

### get module doc
    ansible-doc service

### playbooks

#### execute a playbook
    ansible-playbook web-tls.yml
    # or if the playbook file is executable and starts with `#!/usr/bin/env ansible-playbook`
    ./web-tls.yml
    
handlers should be used only to restart servicesd
WARNING :
  a handler may not be triggered if an error occurs on a task.
  Plus, re-running the play won't help, since the task which notifies the handler won't be executed (no state change)