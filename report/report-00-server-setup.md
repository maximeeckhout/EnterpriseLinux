# Enterprise Linux Lab Report 00

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assignment00:
Een ansible role toevoegen aan de server en een aantal andere zaken installeren op de server.

## Test plan

* Runnen van de test ('test/common.bats')
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


## Test report

Opmerking: in eerste instantie was ik begonnen met de opdracht zonder de ansible rol te gebruiken en dus zelf alles te gaan coderen, hierdoor ben ik natuurlijk wel wat tijd verloren.

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

List all sources of useful information that you encountered while completing this assignment: books, manuals, HOWTO's, blog posts, etc.
* <https://galaxy.ansible.com/bertvv/rh-base>
* <https://docs.ansible.com/ansible/2.5/user_guide/playbooks_reuse_roles.html>
