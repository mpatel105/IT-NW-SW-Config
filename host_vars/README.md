# host_var directory

## naming convention:
* The file should be named [hostname].yml
* Example:
sur-sw-test.yml

## Syntax:
* Available tag for individual task:
    * Base-config:
        * config: deploy base configuration
        * banner: deploy banner configuration

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
    * ipv4:
configuration of IP address. This is currently supported only on 'Vlan' interface
    * reset: [True/False] or not defined
This command will force the interface to be defaulted if set to [True]


## Example:

interfaces:
  GigabitEthernet1/0/1:
    description: test
    switchport_mode: access
    switchport_access_vlan: 8
    switchport_trunk_vlans: 8,24,40,48,169,240
    switchport_trunk_native_vlan: 99
    shutdown: true
    reset: true

  GigabitEthernet1/0/2:
    device_tracking:
      attach_policy: ip_device_tracking_policy
    source_template: TEMPLATE_STANDARD_ENDPOINTS

  GigabitEthernet1/0/3:
    source_template: TEMPLATE_TRUNK_WIFI_AP

  GigabitEthernet1/0/4:
    source_template: TEMPLATE_STANDARD_ENDPOINTS

  GigabitEthernet1/0/48:
    channel_group:
      chg: 1
      mode: active

  Port-channel1:
    description: PO1 test
    switchport_mode: trunk
    switchport_trunk_vlans: 8,24,40,48,169,240
    switchport_trunk_native_vlan: 99  

  Port-channel2:
    description: PO2 test
    switchport_access_vlan: 8
    switchport_mode: access
    reset: true

  Vlan1:
    shutdown: true

  Vlan999:
    ipv4:
      ip: 10.33.0.30
      netmask: 255.255.255.0
