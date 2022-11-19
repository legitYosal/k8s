# Role Name

A Role for configuring netplan and network on a linux system.

## Requirements

- netplan

## Summary

This role will generate netplan configuration file with the given parameters in `netplan_configurations` variable, then copy it to the server and apply it with netplan.  
Note: some of playbooks need to apply netplan changes immediately, so we flush them at the end of the role.
