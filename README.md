# ssh

## Generate keypair
```
ssh-keygen -t rsa -f ~/.ssh/mykey.pem 
```

## ssh config
```
cat 1connectall.sh<<EOF
ssh-agent > ~/agent.sh
source ~/agent.sh
ssh-add ~/.ssh/mykey.pem
ssh-add -l
EOF

cat 2connectall.sh<<EOF
source ~/agent.sh
ssh-add ~/.ssh/mykey.pem
ssh-add -l
EOF

cat ~/.ssh/config<<EOF
Host bastion
  Hostname 192.168.0.10
  User  ec2-user
  #IdentityFile ~/.ssh/mykey.pem
  ForwardAgent yes
  RequestTTY force
  DynamicForward 1234

Host compute1
  Hostname 192.168.0.20
  User ubuntu
  ProxyCommand nc -x localhost:1234
EOF

ssh -A compute1
```

## Finger print aws
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
