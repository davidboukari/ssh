# ssh

### Remove a key in know host list "~/.ssh/known_hosts"

```bash
ssh-keygen -R <ip>
```

### Do not prompt

```bash
ssh -o StrictHostKeyChecking=no <ip>
```
