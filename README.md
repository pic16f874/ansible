# ansible - useful commands

search ssh-public-key in autorized_keys

    ansible hostgroup --forks=1 --become -m shell -a 'executable=/bin/bash cut -d: -f6 /etc/passwd | grep -v "^/$" | while read -r user; do { readlink -e "$user"/.ssh/authorized_keys* | xargs grep -l "ssh-rsa"; } || true; done'
