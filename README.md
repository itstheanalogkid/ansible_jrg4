# Cisco Voice Gateway Configuration Management
## Communication Services


# Theory

This is a work-in-progress collection of Ansible roles designed to manage the Cisco IOS configuration for Communication Services devices:

* Cisco VG204XM
* Cisco VG310
* Cisco VG320

Each role enforces the state of a certain block of configuration. 
However, this is not designed to strip or remove unknown sections of configuration.
It is therefore important not to make ad-hoc changes, lest the device's configuration become unpredictable.

use paramiko for connectivity. The system currently doesn't support standard SSH for Ansible.

# Roles

## IOS Version Management

ios_version - This role will retrieve the IOS version of the device, and compare it to default variable _current_ios_version_. If different, it is indicated on the output report, which is currently text.

### To Do

- [ ] Email report with date and time
- [ ] Variable to trigger downloading new IOS
- [ ] Variable to schedule reload on day delta during maintenance window

## Access Control List Management

cisco_vg_acl - This role will maintain the state of ACLs used by the Cisco VG devices:

- Standard List 10 for SNMP R/O
- Standard List 11 for SNMP R/W and VTY
- Standard List 12 for management SVI
- Standard List 99 for NTP peer list access

At present, this will trigger a config change as the access list changes will be made each time for the remark.

### To Do

- [ ] Fix "remark" ios.config causing changes every time
