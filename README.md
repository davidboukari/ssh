# ssh

### Remove a key in know host list "~/.ssh/known_hosts"

```bash
ssh-keygen -R <ip>
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
