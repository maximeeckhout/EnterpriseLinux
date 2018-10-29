# Enterprise Linux Lab Report 02

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Describe the goals of the current iteration/assignment in a short sentence.
Omschrijving assingment02:
Opzetten van een Master DNS en Slave DNS.

## Test plan

How are you going to verify that the requirements are met? The test plan is a detailed checklist of actions to take, including the expected result for each action, in order to prove your system meets the requirements. Part of this is running the automated tests, but it is not always possible to validate *all* requirements throught these tests.

## Procedure/Documentation

* Hosts pu001 en pu002 toevoegen aan 'vagrant-hosts.yml'
* Hosts pu001 en pu002 toevoegen aan 'site.yml' en toevoegen van de rol bertvv.bind
* Installeren van de rol bertvv.bind
* Aanpassen van de variabelen van de rol

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

## Resources

* <https://galaxy.ansible.com/bertvv/bind>
* <https://serverfault.com/questions/530415/what-is-dns-delegation>
* <https://bertvv.github.io/linux-network-troubleshooting/bind.html>
* <https://support.rackspace.com/how-to/changing-dns-settings-on-linux/>
