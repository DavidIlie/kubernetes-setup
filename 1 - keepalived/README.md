# keepalived

make sure to install keepalived first

```bash
sudo apt install -y keepalived
```

or you can use the ansible playbook in the second page

afterwards copy the two files here to `/etc/keepalived`

ensure that you change in the keepalived config this information below:

-   `state` - can be `MASTER` or `BACKUP`
-   `priority` - make sure master is the highest
-   `virtual_ipaddress` - this will be your load balancer IP
