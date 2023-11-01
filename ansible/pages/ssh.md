- ServerAliveInterval 120
  ServerAliveCountMax 3
  StrictHostKeyChecking no
  UserKnownHostsFile /dev/null
  host github
  	Hostname github.com
  host mivps
  	HostName 167.172.180.49
  	User root
  	IdentityFile ~/.ssh/mivps.pub
  host ansiblemivps
  	HostName 167.172.180.49
  	User ansible
  	IdentityFile ~/.ssh/ansiblemivps.pub
-
- ssh-copy
- sudo apt install software-properties-common -y
-