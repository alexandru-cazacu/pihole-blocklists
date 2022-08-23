# Pi-hole Blocklists

Configuration used on my Pi-hole.

- `distracting.hosts` - might be useful in controlled dosages;
- `always-blocked.hosts` - never useful.

## ROADMAP

- [ ] Add the link to the blog post once it's ready.

## Scripts

`sudo crontab -e` then:

```conf
# m h  dom mon dow   command
0 18 * * * bash -lc /home/pi/unblock-distractions.sh
0 21 * * * bash -lc /home/pi/block-distractions.sh
```

Unblocks distractions from 18:00 to 21:00.

```shell
#!/bin/bash
#
# block-distractions.sh
#
echo 'blocking distractions...'
export PATH="$PATH:/usr/sbin:/usr/local/bin/"
sqlite3 /etc/pihole/gravity.db "update adlist set enabled = true where id = 8;"
pihole restartdns
```

```shell
#!/bin/bash
#
# unblock-distractions.sh
#
echo 'unblocking distractions...'
export PATH="$PATH:/usr/sbin:/usr/local/bin/"
sqlite3 /etc/pihole/gravity.db "update adlist set enabled = false where id = 8;"
pihole restartdns
```

## References

https://thegreata.pe/articles/2021/02/28/pihole/