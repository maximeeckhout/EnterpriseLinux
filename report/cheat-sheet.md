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

| Header One     | Header Two     |
| :------------- | :------------- |
| vagrant status       | Overzicht vagrant omgeving       |
| vagrant up       | Opstarten van Virtuele Machine      |
| vagrant provision       | Draai het config script op VM       |
| vagrant ssh       | Inloggen op VM       |
| vagrant halt       | VM Stoppen       |
| vagrant reload       | VM herstarten       |
| vagrant destroy       | VM vernietiggen       |



## Checklist network configuration

1. Is the IP-adress correct? `ip a`
2. Is the router/default gateway correct? `ip r -n`
3. Is a DNS-server available? `cat /etc/resolv.conf`
