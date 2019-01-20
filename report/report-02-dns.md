# Enterprise Linux Lab Report 02

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assingment02:
Opzetten van een Master DNS en Slave DNS.

## Test plan

Opmerking: Destroy de VM voor het uitvoeren van de testen.

MasterDNS/SlaveDNS:
1. Start de VM op
2. Log in via ssh
3. Pas de variabelen aan in de testen
4. Run de testen ('test/runbats.sh')
5. Testen of het dig commando werkt bij beide servers

## Procedure/Documentation

* Hosts pu001 en pu002 toevoegen aan 'vagrant-hosts.yml'
* Hosts pu001 en pu002 toevoegen aan 'site.yml' en toevoegen van de rol bertvv.bind
* Installeren van de rol bertvv.bind
* Aanpassen van de variabelen van de rol
 * Alle hosts Toevoegen
 * DNS service toestaan voor firewall
 * Zone master ip Instellen
 * Allow query toelaten

## Test report

Problemen:
* In het begin verliep de opdracht moeizaam omdat DNS iets relatief nieuw was, er was dus wel wat extra werk nodig om DNS en de instellingen ervan te begrijpen.

Output test Master DNS en Slave DNS :
```
[vagrant@pu001 ~]$ sudo /vagrant/test/runbats.sh
Running test /vagrant/test/pu001/masterdns.bats
 ✓ The
 ✓ The main config file should be syntactically correct
 ✓ The forward zone file should be syntactically correct
 ✓ The reverse zone files should be syntactically correct
 ✓ The service should be running
 ✓ Forward lookups public servers
 ✓ Forward lookups private servers
 ✓ Reverse lookups public servers
 ✓ Reverse lookups private servers
 ✓ Alias lookups public servers
 ✓ Alias lookups private servers
 ✓ NS record lookup
 ✓ Mail server lookup
```

Dig Commando:
```
dig @192.0.2.10 pu004.avalon.lan
dig @192.0.2.11 pu004.avalon.lan
```

## Resources

* <https://galaxy.ansible.com/bertvv/bind>
* <https://serverfault.com/questions/530415/what-is-dns-delegation>
* <https://bertvv.github.io/linux-network-troubleshooting/bind.html>
* <https://support.rackspace.com/how-to/changing-dns-settings-on-linux/>
