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
