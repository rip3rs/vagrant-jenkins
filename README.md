# Vagrant-Jenkins.
Vagrant box with Nginx Jenkins.

### Prerequisities

`Vagrant`
`virtualbox`

### Instalation

$`vagrant up`

$`sudo vim /etc/hosts`

paste
```
192.168.33.99   jenkins.local.dev
```

### Access Jenkins
`http://jenkins.local.dev`

If by any chance you would like to access jenkins from outside your local machine (lets say git of bitbucket etc...).

In your router assign your machine LAN IP address and port forward 8080:8080, It should access jenkins through your public IP (I don't have to mention the risks... Use this as a dev fun thingy...)
