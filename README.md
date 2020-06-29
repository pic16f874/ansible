### Ansible - useful commands

##### search ssh-public-key in autorized_keys

    ansible hostgroup --forks=1 --become -m shell -a 'executable=/bin/bash cut -d: -f6 /etc/passwd | grep -v "^/$" | while read -r user; do { readlink -e "$user"/.ssh/authorized_keys* | xargs grep -l "ssh-rsa"; } || true; done'

##### Print all crontabs including non-existent users, omitting comments and empty strings

    ansible hostgroup  --forks=1 --become -m shell -a 'executable=/bin/bash ls /var/spool/cron/crontabs | while read -r i; do echo "# Crontab for user $i"; grep -vP "^$|^#" "/var/spool/cron/crontabs/$i"; echo; done'

##### Print timers

    ansible hostgroup --forks=1 --become -m shell -a 'executable=/bin/bash systemctl list-timers --all'

