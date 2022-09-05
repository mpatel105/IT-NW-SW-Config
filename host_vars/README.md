# host_var directory

## naming convention:
* The file should be named [hostname].yml
* Example:
```bash
sur-sw-test.yml
```

## Syntax:
* hostname: [name of device to configure]
  * This value will be the future name of the device when running 'global' tag to reconfigure the device.
  * If this value is not defined, then the inventory_hostname will be used as default

* interfaces:
  * This is the list of all the interfaces as defined on the devices
  * The configuration of each interface can be defined as below:
    * source_template: will be used to configure a template on the interface.
The interface will be defaulted if the configuration on the switch is not the good one.
    * device_tracking:
      * attach_policy: [name of policy to attach]
The device tracking to be configured for IOS-XE devices
    * shutdown: [True/False] or not defined
This will run CLI command 'shutdown' or 'no shutdown' under this interface
    * description:
This will configure a 'description' under this interface
    * switchport_mode: [access] or [trunk]
This will configure the interface either as access or trunk interface
    * switchport_access_vlan: [vlanID]
This will configure the access vlan to be use for mode access
    * switchport_trunk_vlans: [list of vlans to be allowed on trunk]
This is the list of allowed vlans to be used on the trunk interface. *** TO BE TESTED for long list of vlans ***
    * switchport_trunk_native_vlan: [vlanID]
This is the native vlan to be used for the trunk interface
    * channel_group:
Configuration of channel_group to apply on interface
    * spanning-tree_portfast:
Configuration of spanning-tree portfast on interface    
    * ipv4:
configuration of IP address. This is currently supported only on 'Vlan' interface
    * reset: [True/False] or not defined
This command will force the interface to be defaulted if set to [True]


## Example:

* interface configuration with mode access in vlan 8 , portfast enabled, shutdown, description 'test'. the interface will be forced to be defaulted with 'reset: true'
```bash
interfaces:
  GigabitEthernet1/0/1:
    description: test
    switchport_mode: access
    switchport_access_vlan: 8
    shutdown: true
    spanning-tree_portfast: true
    reset: true
```

* interface configuration defaulted with mode trunk :
```bash

  GigabitEthernet1/0/1:
    description: test
    switchport_mode: trunk
    switchport_trunk_vlans: 8,24,40,48,169,240
    switchport_trunk_native_vlan: 99
    spanning_tree_portfast: false
    shutdown: false
```
* interface configuration with source template and device tracking configured
```bash
  GigabitEthernet1/0/2:
    device_tracking:
      attach_policy: ip_device_tracking_policy
    source_template: TEMPLATE_STANDARD_ENDPOINTS
```
* interface configuration with source template only
```bash
  GigabitEthernet1/0/3:
    source_template: TEMPLATE_TRUNK_WIFI_AP
```
* interface configuration with source template only
```bash
  GigabitEthernet1/0/4:
    source_template: TEMPLATE_STANDARD_ENDPOINTS
```
* interface configuration with channel-group
```bash
  GigabitEthernet1/0/48:
    channel_group:
      chg: 1
      mode: active
```
* interface configuration for trunk Port-Channel configuration
```bash
  Port-channel1:
    description: PO1 test
    switchport_mode: trunk
    switchport_trunk_vlans: 8,24,40,48,169,240
    switchport_trunk_native_vlan: 99  
```
* interface configuration for access Port-Channel configuration
```bash
  Port-channel2:
    description: PO2 test
    switchport_access_vlan: 8
    switchport_mode: access
    reset: true
```
* interface configuration for vlan1 shutdown
```bash
  Vlan1:
    shutdown: true
```
* interface configuration for vlan configuration with description and ip address defined
```bash
  Vlan999:
    description: test vlan
    ipv4:
      ip: 10.33.0.30
      netmask: 255.255.255.0
```

## Full Example:

```bash
hostname: sur-sw-test2

interfaces:
    GigabitEthernet0/0:
        negotiation_auto: true
        shutdown: true
        vrf: Mgmt-vrf
    GigabitEthernet1/0/1:
        description: test
        switchport_mode: access
        switchport_access_vlan: 8
        spanning_tree_portfast: false
        shutdown: true
        reset: true
    GigabitEthernet1/0/10:
        device_tracking:
          attach_policy: ip_device_tracking_policy
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/11:
        source_template: TEMPLATE_TRUNK_WIFI_AP
    GigabitEthernet1/0/12:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/13:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/14:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/15:
        source_template: TEMPLATE_TRUNK_WIFI_AP
    GigabitEthernet1/0/16:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/17:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/18:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/19:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/2:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/20:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/21:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/22:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/23:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/24:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/25:
    GigabitEthernet1/0/26:
    GigabitEthernet1/0/27:
    GigabitEthernet1/0/28:
    GigabitEthernet1/0/29:
    GigabitEthernet1/0/3:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/30:
    GigabitEthernet1/0/31:
    GigabitEthernet1/0/32:
    GigabitEthernet1/0/33:
    GigabitEthernet1/0/34:
    GigabitEthernet1/0/35:
    GigabitEthernet1/0/36:
    GigabitEthernet1/0/37:
    GigabitEthernet1/0/38:
    GigabitEthernet1/0/39:
    GigabitEthernet1/0/4:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/40:
    GigabitEthernet1/0/41:
    GigabitEthernet1/0/42:
    GigabitEthernet1/0/43:
    GigabitEthernet1/0/44:
    GigabitEthernet1/0/45:
    GigabitEthernet1/0/46:
    GigabitEthernet1/0/47:
    GigabitEthernet1/0/48:
        channel_group:
            chg: 1
            mode: active
        switchport_mode: trunk
    GigabitEthernet1/0/5:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/6:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/7:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/8:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/0/9:
        source_template: TEMPLATE_STANDARD_ENDPOINTS
    GigabitEthernet1/1/1:
    GigabitEthernet1/1/2:
    GigabitEthernet1/1/3:
    GigabitEthernet1/1/4:
    Port-channel1:
        switchport_mode: trunk
    Port-channel2:
        description: po2 test2
        switchport_mode: trunk
        switchport_trunk_vlans: 8,24,40,48,169,240
        switchport_trunk_native_vlan: 99
    Port-channel3:
        description: PO3 test3
        switchport_access_vlan: 8
        switchport_mode: access
    Vlan1:
        shutdown: true
    Vlan999:
        ipv4:
            ip: 10.33.0.30
            netmask: 255.255.255.0
    Vlan190:
        shutdown: false
        reset: true
        ipv4:
            ip: 10.33.190.30
            netmask: 255.255.255.0

```
