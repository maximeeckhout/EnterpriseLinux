# Enterprise Linux Lab Report 03

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assignment03:
- Opzetten van Samba file server
- Opzetten van FTP Server met Vsftpd
- Toegang tot bestanden en mappen beheren
- Gebruik maken van SELinux

## Test plan

We kunnen deze opdracht testen door via Files naar 'smb://files/' te gaan en 'ftp://files/' daar zouden de shares terug te vinden moeten zijn en beschikbaar voor de juiste gebruikers.

## Procedure/Documentation


* Toevoegen van pr011 aan ```vagrant-hosts.yml```
* Toevoegen van pr011 aan ```site.yml``` en toevoegen van de rollen:
  - bertvv.rh-base
  - bertvv.samba
  - bertvv.vsftpd
* Installeren van alle ansible rollen.
* Variabelen aanpassen van de rollen
 * Aanmaken van rh-base users
 * Aanmaken van Samba users
 * Aanmaken van Samba shares
 * Instellen van de juiste rechten op de shares
 * Services toelaten bij firewall


## Test report

```
[vagrant@pr011 ~]$ sudo /vagrant/test/runbats.sh
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
Running test /vagrant/test/pr011/samba.bats
 ✓ The ’nmblookup’ command should be installed
 ✓ The ’smbclient’ command should be installed
 ✓ The Samba service should be running
 ✓ The Samba service should be enabled at boot
 ✓ The WinBind service should be running
 ✓ The WinBind service should be enabled at boot
 ✓ The SELinux status should be ‘enforcing’
 ✓ Samba traffic should pass through the firewall
 ✓ Check existence of users
 ✓ Checks shell access of users
 ✓ Samba configuration should be syntactically correct
 ✓ NetBIOS name resolution should work
 ✓ read access for share ‘public’
 ✓ write access for share ‘public’
 ✓ read access for share ‘management’
 ✓ write access for share ‘management’
 ✓ read access for share ‘technical’
 ✓ write access for share ‘technical’
 ✓ read access for share ‘sales’
 ✓ write access for share ‘sales’
 ✓ read access for share ‘it’
 ✓ write access for share ‘it’

22 tests, 0 failures
Running test /vagrant/test/pr011/vsftp.bats
 ✓ VSFTPD service should be running
 ✓ VSFTPD service should be enabled at boot
 ✓ The ’curl’ command should be installed
 ✓ The SELinux status should be ‘enforcing’
 ✓ FTP traffic should pass through the firewall
 ✓ VSFTPD configuration should be syntactically correct
 ✓ Anonymous user should not be able to see shares
 ✓ read access for share ‘public’
 ✓ write access for share ‘public’
 ✓ read access for share ‘management’
 ✓ write access for share ‘management’
 ✓ read access for share ‘technical’
 ✓ write access for share ‘technical’
 ✓ read access for share ‘sales’
 ✓ write access for share ‘sales’
 ✓ read access for share ‘it’
 ✓ write access for share ‘it’

17 tests, 0 failures
```

## Resources

* <https://galaxy.ansible.com/bertvv/vsftpd>
* <https://galaxy.ansible.com/bertvv/samba>
