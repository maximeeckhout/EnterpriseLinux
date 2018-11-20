# Cheat sheets and checklists

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

## Basic commands

| Task                | Command |
| :---                | :---    |
| Query IP-adress(es) | `ip a`  |

## Git workflow

Simple workflow for a personal project without other contributors:

| Task                                         | Command                   |
| :---                                         | :---                      |
| Current project status                       | `git status`              |
| Select files to be committed                 | `git add FILE...`         |
| Commit changes to local repository           | `git commit -m 'MESSAGE'` |
| Push local changes to remote repository      | `git push`                |
| Pull changes from remote repository to local | `git pull`                |

## Vagrant

| Code    | Task     |
| :------------- | :------------- |
| vagrant status       | Overzicht vagrant omgeving       |
| vagrant up       | Opstarten van Virtuele Machine      |
| vagrant provision       | Draai het config script op VM       |
| vagrant ssh       | Inloggen op VM (naam meegeven bij meerdere VM's)      |
| vagrant halt       | VM Stoppen       |
| vagrant reload       | VM herstarten       |
| vagrant destroy       | VM vernietiggen       |

## MariaDB

| Code    | Task     |
| :------------- | :------------- |
| mysql -u root -p       |Inloggen als root bij MariaDB       |
| Select user, host from mysql.user;      | Query om de users te zien      |
| select user, db, host, password from mysql.db;       | Query om databanken te zien      |


## Setting up an SSL secured Webserver with CentOS
```
# Generate private key
openssl genrsa -out ca.key 2048

# Generate CSR
openssl req -new -key ca.key -out ca.csr

# Generate Self Signed Key
openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt

# Copy the files to the correct locations
cp ca.crt /vagrant/ansible/files/
cp ca.key /vagrant/ansible/files/
cp ca.csr /vagrant/ansible/files/
```

## Checklist network configuration

1. Is the IP-adress correct? `ip a`
2. Is the router/default gateway correct? `ip r -n`
3. Is a DNS-server available? `cat /etc/resolv.conf`

## Create SHA512 password hashes on command line

```
meeckhout@Dell-Maxim:~$ mkpasswd -m sha-512
```

## Get a new DHCP Lease
```
sudo dhclient -r
sudo dhclient
```
