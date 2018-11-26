# Enterprise Linux Lab Report 01

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assingment01:
Opzetten van een LAMP (Apache,MariaDB,PHP) op de server en Wordpress installeren.

## Test plan

Apache :
* De Apache-test pagina zou zichtbaar moeten zijn als je in de host-browser naar het IP-adres van de VM gaat.
* Service moet active zijn
* Firewall moet correct ingesteld zijn zodat de site voor de host bereikbaar is

MariaDB:
* Er zal een database aangemaakt moeten worden voor de Wordpress
* Er zal een user moeten terug te vinden zijn in deze db

PHP:
* Moet beschikbaar zijn op de VM

Runnen van de automated tests.

## Procedure/Documentation

* Apache, MariaDB en Wordpress installeren door de rollen 'bertvv.httpd','bertvv.mariadb'en ''bertvv.wordpress'' toe te voegen aan 'site.yml'-file
* Runnen van het 'role-deps.sh' script zodat deze rollen geinstalleerd worden.
* Vervolgens moesten enkele variabelen aangepast om alles werkende te krijgen.

## Test report

Problemen:
* Ik kreeg lange tijd een 'error establishing a database connection'-error doordat ik de credentials verkeerd had ingesteld.
* Ook had ik een host ip ingesteld voor MariaDB en was dit niet nodig, hierdoor kon ik natuurlijk ook niet aan de pagina.
* Ook kreeg ik vaak volgende error, deze is maar gedeeltelijk opgelost.
```
[pu004] GuestAdditions versions on your host (5.2.20) and guest (5.2.18) do not match.
```

Output van het testscript:
```
[maxim@pu004 ~]$ /vagrant/test/runbats.sh
Running test /vagrant/test/pu004/lamp.bats
 ✓ The necessary packages should be installed
 ✓ The Apache service should be running
 ✓ The Apache service should be started at boot
 ✓ The MariaDB service should be running
 ✓ The MariaDB service should be started at boot
 ✓ The SELinux status should be ‘enforcing’
 ✓ Web traffic should pass through the firewall
 ✓ Mariadb should have a database for Wordpress
 ✓ The MariaDB user should have write
 ✓ The website should be accessible through HTTP
 ✓ The website should be accessible through HTTPS
 ✓ The certificate should not be the default one
 ✓ The Wordpress install page should be visible under http://192.0.2.50/wordpress/
 ✓ MariaDB should not have a test database
 ✓ MariaDB should not have anonymous users

15 tests, 0 failures
```

## Resources

* <https://mariadb.com/kb/en/library/grant/>
* <https://www.cyberciti.biz/faq/how-to-show-list-users-in-a-mysql-mariadb-database/>
* [bertvv.httpd](https://galaxy.ansible.com/bertvv/httpd)
* [bertvv.mariadb](https://galaxy.ansible.com/bertvv/mariadb)
* <https://github.com/bertvv/ansible-role-wordpress/blob/vagrant-tests/test.yml>
* [bertvv.wordpress](https://galaxy.ansible.com/bertvv/wordpress)
* https://wiki.centos.org/HowTos/Https
