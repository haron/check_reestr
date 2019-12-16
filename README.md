# Russian

Это плагин для Nagios/Icinga, который проверяет, попадают ли ваши IP в список заблокированных Роскомнадзором адресов и подсетей.

# Prerequisites

Python 3 and `requests` module installed. For Ubuntu:

    sudo apt-get -y install python3-requests

# Example

    > ./check_reestr t.me flibusta.is
    Hosts found in RKN registry: t.me (149.154.167.99), flibusta.is (81.17.19.227). Verify at https://blocklist.rkn.gov.ru

# Usage options

    > ./check_reestr -h
    usage: check_reestr [-h] [-i INVENTORY] [-r REESTR] [-x EXCLUDE] [host [host ...]]

    positional arguments:
      host                  hosts to check (default: [])

    optional arguments:
      -h, --help            show this help message and exit
      -i INVENTORY, --inventory INVENTORY
                            Ansible inventory URL (hosts will be added to the list) (default: None)
      -r REESTR, --reestr REESTR
                            RKN registry URL (default: https://api.reserve-rbl.ru/api/v2/ips/json)
      -x EXCLUDE, --exclude EXCLUDE
                            ignore hosts, e.g. -x host1,host2,... (default: set())

If you have a [dynamic Ansible inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html) somewhere in your infrastructure, you can use it directly:

    > ./check_reestr -i http://your.inventory/data.json

# WARNING

Running this script frequently will cause excessive load to RosKomSvoboda infrastructure. Run it once in 4-12 hours.
