# ssh

## Finger print
```
for key in *.pem
do
  echo $key
  ssh-keygen -lf $key
  ssh-keygen -lf $key -E md5
  ssh-keygen -lf $key -m pkcs8 | openssl pkey -pubin -outform der | openssl md5 -c
  openssl pkcs8 -in $key -inform PEM -outform DER -topk8 -nocrypt | openssl sha1 -c
done
```

### Remove a key in know host list "~/.ssh/known_hosts"

```bash
ssh-keygen -R <ip>

ssh-keygen -f "/root/.ssh/known_hosts" -R 10.1.1.3
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
