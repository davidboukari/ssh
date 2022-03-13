# ssh

### Remove a key in know host list "~/.ssh/known_hosts"

```bash
ssh-keygen -R <ip>
```
### generate a public key from a private key

```bash
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```

### Do not prompt

```bash
ssh -o StrictHostKeyChecking=no <ip>
```

## secure sshd

### use knockd

```bash
cat /etc/ssh/sshd_config

Protocol 2
#Avoid port 22
```
## Set identityFile
```
cat ~/ssh/config
Host myhostserver
  Hostname xxx.xxx
  User myuser
  IdentityFile ~/.ssh/mykey.pem
```

## ssh with bastion
```
ssh -J ubuntu@192.168.0.54   ubuntu@192.168.1.1

ssh -J ubuntu@192.168.0.119 ubuntu@10.0.0.31
ssh ubuntu@192.168.0.119  -Y ssh -tt ubuntu@10.0.0.31
```
