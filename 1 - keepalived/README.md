# keepalived

make sure to install keepalived first

```bash
sudo apt install -y keepalived
```

afterwards copy the two files here to `/etc/keepalived`

ensure that you change in the keepalived config the the:

- state - can be `MASTER` or `BACKUP`
- priority - make sure master is the highest