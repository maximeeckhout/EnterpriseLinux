# Enterprise Linux Extra

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving:
* Fail2Ban
* Ansible sneller maken
* Ansible Vault

## Procedure/Documentation

### Fail2Ban

Deze rol voegen we toe aan pu004 zodat we deze beter kunnen beveiligen.

### Ansible versnellen

#### Tijd zonder aanpassingen

![Tijd](pictures/tijdAnsible)

Door in de ansible.cfg file een wijzig aan te brengen kunnen we timen hoe lang elke stap duurt. Deze tijd zullen we dus proberen te verkleinen

#### SSH Pipelining
We wijzigen in ansible.cfg
```
[ssh_connection]
pipelining = True
```
#### ControlPersist
```
[ssh_connection]
pipelining = True
control_path = /tmp/ansible-ssh-%%h-%%p-%%r
```

### Ansible Vault

Ansible Vault wordt gebruikt om op een betere manier om te gaan met wachtwoorden, het zorgt ervoor dat de wachtwoorden niet op git komen.

## Test report

### Fail2Ban
Test: Wanneer men meerdere malen probeert in te loggen met foutieve gegevens zou dit ip address geblokkeerd moeten worden.
Resultaat:

### Ansible versnellen
Test: Na de aanpassingen zou Ansible sneller moeten runnen dan de oorspronkelijk.
Resultaat:

### Ansible Vault
Test: Alle wachtwoorden worden nu bijhouden volgens het principe van de Ansible Vault.
Resultaat:

## Resources

* <https://docs.ansible.com/ansible/latest/installation_guide/intro_configuration.html>
* <https://github.com/jlafon/ansible-profile>
* <https://adamj.eu/tech/2015/05/18/making-ansible-a-bit-faster/>
* <https://github.com/nbigot/ansible-fail2ban>
* <https://acalustra.com/acelerate-your-ansible-playbooks-with-async-tasks.html>
* <https://docs.ansible.com/ansible/2.4/vault.html>
