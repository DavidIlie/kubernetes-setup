# ansible setup

must: make sure you set the hosts.ini and change the load balancer ip where it needs to be changed in `install-k3s.yml`
must 2: create a custom secret for the masters

command to install:

```bash
ansible-playbook install-k3s.yml --user david --ask-become-pass -i hosts.ini
```

```bash
ansible-playbook uninstall-k3s.yml --user david --ask-become-pass -i hosts.ini
```

if you want to do step 7 (provision nfs volumes)

```bash
ansible-playbook uninstall-nfs.yml --user david --ask-become-pass -i hosts.ini
```
