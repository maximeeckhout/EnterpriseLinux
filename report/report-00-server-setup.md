# Enterprise Linux Lab Report 00

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assignment00:
Een ansible role toevoegen aan de server en een aantal andere zaken installeren op de server.

## Test plan

Opmerking: Destroy de VM voor het uitvoeren van de testen.

1. Start de VM op
2. Log in via ssh
3. Pas de variabelen aan in de testen
4. Run de testen ('test/runbats.sh')
  * SELinux should be set to 'Enforcing'
  * Firewall should be enabled and running
  * EPEL repository should be available
  * Bash-completion should have been installed
  * bind-utils should have been installed
  * Git should have been installed
  * Nano should have been installed
  * Tree should have been installed
  * Vim-enhanced should have been installed
  * Wget should have been installed
  * Admin user maxim should exist
  * An SSH key should have been installed for maxim
  * Custom /etc/motd should have been installed

## Procedure/Documentation

* Installeren van alle nodige software (vooral ansible moest geinstalleerd worden)
* Bestuderen van de ansible rol ('bertvv.rh-base' <https://galaxy.ansible.com/bertvv/rh-base>)
* Aanpassen van de 'site.yml'-file gebruikmakend van de ansible rol
* Opstarten van de virtuele machine met 'Vagrant up' (let op dat de provisioning gebeurt)
* Testen of alles werkt en het testscript runnen, waar nodig bij sturen of de 'site.yml' aanpassen.

Opmerkingen:
* Het passwoord voor de rh-base user moet gehashed zijn, dit kan via het commando: ```meeckhout@Dell-Maxim:~$ mkpasswd -m sha-512```
* Een gebruiker kan je admin maken door hem toe te voegen aan de groep "wheel"
* ondertussen zijn de variabelen specifiek voor een bepaalde host verplaatst naar ```ansible/host_vars/pu004.yml```
* de globale variabelen zijn te vinden in ```ansible/group_vras/all.yml```

## Test report

Opmerking: in eerste instantie was ik begonnen met de opdracht zonder de ansible rol te gebruiken en dus zelf alles te gaan coderen, hierdoor ben ik natuurlijk wel wat tijd verloren.

1. Start de VM met ```vagrant up pu004```
2. Log in: ```vagrant ssh pu004```
3. Pas de variabelen aan in ```test/pu004/lamp.bats```
4. Run de testen
Output van het testscript:
```
[maxim@pu004 ~]$ /vagrant/test/runbats.sh
Running test /vagrant/test/common.bats
 ✓ SELinux should be set to 'Enforcing'
 ✓ Firewall should be enabled and running
 ✓ EPEL repository should be available
 ✓ Bash-completion should have been installed
 ✓ bind-utils should have been installed
 ✓ Git should have been installed
 ✓ Nano should have been installed
 ✓ Tree should have been installed
 ✓ Vim-enhanced should have been installed
 ✓ Wget should have been installed
 ✓ Admin user maxim should exist
 ✓ An SSH key should have been installed for maxim
 ✓ Custom /etc/motd should have been installed

13 tests, 0 failures
```
## Resources

* <https://galaxy.ansible.com/bertvv/rh-base>
* <https://docs.ansible.com/ansible/2.5/user_guide/playbooks_reuse_roles.html>
