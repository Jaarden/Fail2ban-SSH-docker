# Fail2ban-SSH-docker
Connect fail2ban to an openssh docker container

Create a local jail file

```
vm /etc/fail2ban/jail.local
```
Add the following and replace ` $PATH_TO_DOCKER_SSH_LOG` with the path to your OpenSSHserver logging

```
[sshd]
enabled = true
port = 22
filter = sshd
logpath = $PATH_TO_DOCKER_SSH_LOG
maxretry = 3
#use bantime -1 for perm ban
bantime  = 600
findtime = 600
action = iptables-allports[actname=sshd,name=sshd,protocol=all]
         iptables-allports[actname=sshd-docker,name=sshd-docker,protocol=all,chain=DOCKER]
```


```
sudo service fail2ban restart
```
