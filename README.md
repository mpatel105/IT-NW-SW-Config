# IT-Network-switch-base-config

## Network ansible playbook
* Exiting roles:
    * Base-config: deploy base configuration on switches
    * NAC-config: deploy NAC configuration on switches
    * Inventory: Create a inventory.csv file on GIT Repo IT-Network-Scripts

* Available tag for individual task:
    * Base-config:
        * config: deploy base configuration
        * banner: deploy banner configuration
        * configadminuser: configure local admin user & enable password with level 9 (scrypt) algorythm
        * configenable: configure enable password with level 9 (scrypt) algorythm
        * configvlan: deploy vlan configuration
        * configswitchports8: configure interface for vlan 8
        * configswitchports2448: configure interface for vlan 24 & 48
        * configswitchports24: configure interface description only for vlan 24 (add a tag 'VLAN24' on the interface description)
        * configswitchports48: configure interface description only for vlan 48 (add a tag 'VLAN48' on the interface description)
        * configswitchportswifi: configure interface for WIFI Access Point
        * configusers: configure credential on the switch
        * clock: deploy clock configuration
        * disableaux: disable Line AUX
        * dns: deploy dns configuration
        * intdescr: configure interface description from CDP (need newer Ansible version platform is not present from neighbors with current version)
        * logs: deploy logs configuration
        * ntp: deploy ntp configuration
        * radius: configure Radius on the switch
        * removecredentials: Remove all credentials like ssh pubkey-chain, ftp, enable password
        * removelocalusers: Remove all local users except admin
        * saveconfig: save configuration to NVRAM
        * services: enable/disable standard IOS services
        * snmp: configure SNMP details
        * ssh: deploy SSH configuration
        * STPaccess: deploy Spanning-Tree configuration for ACCESS Switches only
        * STPcore: deploy Spanning-Tree configuration for CORE Switches only
    * NAC-config:
        * NACconfig: deploy NAC configuration
        * NACglobal: deploy NAC global configuration only
        * NACint: deploy NAC interface configuration only
    * Inventory:
        * inventory: Create the inventory.csv file on GIT repo IT-Network-Scripts
