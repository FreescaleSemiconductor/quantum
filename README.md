
VXLAN Support for Quantum
=========================

This code provides vxlan support for openvswitch in stable/folsom. 
## Requirements ##
* VXLAN support in OVS at
```
https://github.com/FreescaleSemiconductor/ovs-vxlan
```
* Currently, VXLAN only supports multicast based learning. A multicast IP
address is required.

## How to Use ##

```
git clone https://github.com/FreescaleSemiconductor/quantum.git

git checkout stable/folsom
```

* set the tenant_network_type to vxlan.
* configure the multicast ip with mcast_ip
* configure an interface to send and receive the multicast messages with
 mcast_routing_interface

```
# Sample ovs_quantum_plugin.ini config file #
[DATABASE]
sql_connection = mysql://openstack:openstack@172.16.1.1:3306/quantum
reconnect_interval = 2

[OVS]
network_vlan_ranges = 
bridge_mappings = 
tenant_network_type = vlan
enable_tunneling = True
tunnel_id_ranges = 1:1000
integration_bridge = br-int
tunnel_bridge = br-tun
mcast_ip = 224.0.0.55
mcast_routing_interface = eth0

[AGENT]
polling_interval = 2
root_helper = sudo /usr/bin/quantum-rootwrap /etc/quantum/rootwrap.conf
```
