# Enterprise Linux Lab Report - Troubleshooting

- Student name: Maxim Eeckhout
- Class/group: TIN-TI-3B (Gent)

## Instructions

- Write a detailed report in the "Report" section below (in Dutch or English)
- Use correct Markdown! Use fenced code blocks for commands and their output, terminal transcripts, ...
- The different phases in the bottom-up troubleshooting process are described in their own subsections (heading of level 3, i.e. starting with `###`) with the name of the phase as title.
- Every step is described in detail:
    - describe what is being tested
    - give the command, including options and arguments, needed to execute the test, or the absolute path to the configuration file to be verified
    - give the expected output of the command or content of the configuration file (only the relevant parts are sufficient!)
    - if the actual output is different from the one expected, explain the cause and describe how you fixed this by giving the exact commands or necessary changes to configuration files
- In the section "End result", describe the final state of the service:
    - copy/paste a transcript of running the acceptance tests
    - describe the result of accessing the service from the host system
    - describe any error messages that still remain

## Report

### Phase 1: Physical and Network Access layer

In deze fase wordt de netwerk hardware getest en kijken we of er een IP-address is

| Test                                      | Status      |
| :---                                      | :---        |
| Staat de machine aan                      | CHECK           |
| Kabel aangesloten (VirtualBox)             | CHECK     |
| Correcte netwerkinstellingen (VirtualBox) | CHECK     |
| Interface is up (3)  |    FOUT => interface is down       |

#### Kabel aangesloten
* VirtualBox > VM > Machine Tools > Settings > Network > Advanced > Cable Connected

#### VirtualBox netwerkinstellingen
* VirtualBox  > Global Tools > Check Adapter Settings

#### Interface up
```
[vagrant@nginx ~]$ ip -c address
```
=> Zou up moeten teruggeven, NO-carrier betekent dat er geen signaal is op deze interface.

(Option "-c" zorgt voor leesbaarheid, vershillende belangrijke variabelen woorden dan in een kleur gezet)

#### Fouten in deze fase
| Fout    | Oplossing |
| :---    | :---      |
| Fout 1  | Interface is down          |


### Phase 2: Internet layer

In deze fase wordt getest of het IP-address corect toegekend is en of de default gateway en DNS ingesteld zijn.

| Test                                      | Status      |
| :---                                      | :---        |
| Configuratie IP correct                   | FOUT            |
| IP-address is de verwachtte waarde        | CHECK            |
| Default Gateway ingesteld en correct      | CHECK           |
| DNS ingesteld en correct                  | CHECK            |
| VM bereikbaar van host                    | FOUT => doordat er nog  geen IP is          |
| Controleren DNS name resolution          | FOUT             |

#### IP-address
##### Config file
Controleren van: ```/etc/sysconfig/network-scripts/ifcfg-XXX```
Verwachtingen in deze file:
* DHCP
  * Device = interface naam
  * Onboot = yes
  * BOOTPROTO = dhcp
* Static IP
  * Device = interface naam
  * Onboot = yes
  * BOOTPROTO = none
  * IPADDR moet ingesteld zijn
  * NETMASK moet ingesteld zijn

#### Waarde van IP-address
Controleren met: ```ip -c a```
Verwachtingen:
* IP-address is "192.168.56.42"

Mogelijke problemen:
* Geen IP
  * Is de DHCP server bereikbaar?
* IP toegekend, maar niet de verwachtte waarde
  * Controleren of IP niet statisch toegekend is => config file bekijken

#### Default Gateway
Controleren met: ```ip route```
Verwachtingen:
* Commando geeft de juiste Default Gateway terug

Mogelijke problemen:
* Geen Default Gateway
  * DHCP Server correct geconfigureerd?
* Verkeerde waarde
  * DHCP Server correct geconfigureerd?

#### DNS
Controleren in: ```/etc/resolv.conf```
Verwachtingen:
* Vinden het IP-address van de DNS Server niet/verkeerd terug
  * Aanpassen van de file
  * Voorbeeld
  ```
  nameserver 192.168.10.12
  ```
#### VM bereikbaar vanaf host
Controler met: ```ping 192.168.56.42```
Verwachtingen:
* We krijgen replies

#### DNS Name Resolution
Verwachtingen:
* DNS antwoord correct op aanvragen clients

Controleren:
* DNS antwoord correct
```
$ dig XXXX @192.168.56.42
```
!! Installeer "bind-utils" voor dig, als dit niet mogeijk is gebruik ```getent ahosts www.example.be```

#### Herstarten netwerk na wijzigingen
Commando:
```
systemctl restart network
```

#### Fouten in deze fase
| Fout    | Oplossing |
| :---    | :---      |
| Onboot verkeerd  |Onboot op on zetten en opnieuw opstarten, VM ook bereikbaar van op host   |


### Phase 3: Transport layer

Verwachtingen:
* Firewall is correct geconfigureerd en werkt

Controleren:
* DNS = port 53 (!! udp + tcp)
```
ss -tlnp
ss -ulnp
```
* Draait de Firewall?
```
[vagrant@nginx ~]$ sudo systemctl status firewalld
```
* Firewall Config
```
[vagrant@nginx ~]$ sudo firewall-cmd --list-all
```
* Poort toevoegen
```
[vagrant@nginx ~]$ sudo firewall-cmd --add-service=https --permanent
[vagrant@nginx ~]$ sudo firewall-cmd --reload
[vagrant@nginx ~]$ sudo firewall-cmd --list-all
```

#### Fouten in deze fase
| Fout    | Oplossing |
| :---    | :---      |
| DNS niet toegevoegd aan firewall  | Toevoegen van dns service aan firewall  |

```
[vagrant@nginx ~]$ sudo firewall-cmd --add-service=dns --permanent
[vagrant@nginx ~]$ sudo firewall-cmd --reload
[vagrant@nginx ~]$ sudo firewall-cmd --list-all
```

### Phase 4: Application layer

Verwachtingen:
* Syntax van config bestanden is correct
* Syntax zonebestanden is correct
* DNS antwoord correct op aanvragen clients
* Named service is correct geconfigureerd en werkt

Controleren:
* Status van Named bekijken
```
systemctl status named
```
* Named service starten
```
systemctl start named
```
* Syntax config bestanden
```
$ sudo named-checkconf /etc/named.conf
```
* Syntax zone zonebestanden
```
$ sudo named-checkzone linuxlab.lan /var/named/linuxlab.lan
$ sudo named-checkzone 15.168.192.in-addr.arpa \ /var/named/15.168.192.in-addr.arpa
```

output:
```
[root@golbat named]# named-checkzone 192.168.56.in-addr.arpa \ 192.168.56.in-addr.arpa
zone 192.168.56.in-addr.arpa/IN: loading from master file  192.168.56.in-addr.arpa failed: file not found
zone 192.168.56.in-addr.arpa/IN: not loaded due to errors.

```
* Logs bekijken (best in andere terminal)
```
$ sudo rndc querylog on
$ sudo journalctl -l -f -u named.service
$ sudo systemctl status named
```
* DNS antwoord correct
```
$ dig 192.168.10.10 @192.168.56.42
```
* DNS antwoord correct (reverse lookup)
```
$ dig -x www.test.be  @192.168.56.42
```
Opmerkingen:
* FQDN moeten eindigen met een "." => "example.com."
* named.conf verwachtte waarden:
  * listen-on port 53 { 127.0.0.1; **192.168.1.101;**}; // **Master** DNS IP
  * allow-query     { localhost; **192.168.1.0/24;**}; // IP Range
  *  allow-transfer{ localhost; **192.168.1.102;** };   // **Slave** DNS IP
* Zone naamging => IP-address omdraaien en netwerkgedeelte weglaten
  * 192.168.10.0/24 => 10.168.192.XXXX

#### Fouten in deze fase
| Fout    | Oplossing |
| :---    | :---      |
| Origin in 56.168.192.in-addr.arpa. is verkeerd   | Moest $ORIGIN 56.168.192.in-addr.arpa. zijn      |
| Verkeerde IP addresen voor butterfree en beedle    | .12 en .13 omwisselen in cynalco.com en 56.168.192.in-addr.arpa  |
| Fout in named.conf |Luistert niet op 192.168.56.42 => listen-on port 53 { 127.0.0.1; 192.168.56.42; };|
| 2de NS server werd niet gevonden  | Toevoegen van NS record in cynalco.com         |

## End result

```
[root@golbat vagrant]# ./acceptance_test.bats
 ✓ Forward lookups private servers
 ✓ Forward lookups public servers
 ✓ Reverse lookups private servers
 ✓ Reverse lookups public servers
 ✓ Alias lookups private servers
 ✓ Alias lookups public servers
 ✓ NS record lookup
 ✓ Mail server lookup

8 tests, 0 failures
```
## Resources

* [Slides Github](https://hogenttin.github.io/elnx-syllabus/troubleshooting/#/title-slide)
* [Linux Troubleshooting](https://github.com/bertvv/linux-network-troubleshooting)
* [Setting Up DNS Server](https://www.unixmen.com/setting-dns-server-centos-7/)
