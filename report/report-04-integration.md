# Enterprise Linux Lab Report 04

- Student name: Maxim Eeckhout
- Github repo: <https://github.com/HoGentTIN/elnx-1819-sme-maximeeckhout>

Omschrijving assignment04:
- Opzetten van DHCP server
- Instellen van een router met vyos

## Test plan

Opmerking: Destroy de VM voor het uitvoeren van de testen.

- Opzetten van een virtuele machine met 2 host-only netwerk interfaces (beide verbonden met het host-only netwerk 172.16.0.0./16)
- Onthouden van 1 van de 2 MAC adressen van de interfaces
- VM opstarten en controleren welk IP-address wordt toegekend aan welke interface
- Controleren of de VM kan surfen naar <http://www.avalon.lan>
- Controleren of de VM de fileserver kan bereiken via SMB en FTP

## Procedure/Documentation

Describe *in detail* how you completed the assignment, with main focus on the "manual" work. It is of course not necessary to copy/paste your code in this document, but you can refer to it with a hyperlink.

Make sure to write clean Markdown code, so your report looks good and is clearly structured on Github.

## Test report

The test report is a transcript of the execution of the test plan, with the actual results. Significant problems you encountered should also be mentioned here, as well as any solutions you found. The test report should clearly prove that you have met the requirements.

## Resources

* <https://vyos.io>
* <https://wiki.vyos.net/wiki/User_Guide>
* <https://galaxy.ansible.com/bertvv/dhcp>
