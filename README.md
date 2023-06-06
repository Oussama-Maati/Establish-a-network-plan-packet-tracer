Group Project : Establish a network plan
========================================

_Team : 4 person_
_Delay : 3 Days_

# How to :

First of all we made a plan of the futur network, giving a subnet for each department:

| Subnet     | IP Range        | Number of Posts |
|------------|-----------------|-----------------|
| Management | 192.168.10.0    | 5               |
| Production | 192.168.20.0    | 10              |
| Study      | 192.168.30.0    | 8               |
| Support    | 192.168.40.0    | 2x30            |
| Server     | 192.168.60.0    | 3               |


Then on cisco we put our main router and a switch (for each subnet) directly connected to him. For the support department due of a large number of pc we add two other switch, one for each sector, and then connect those to the switch connected to the router.And finaly we add the end devices asked for each department.

# Configuration :


## Main router
Set the correct ip on each port, those ip gonna be the DEFAULT GATEWAY for each subnet.
| Subnet     | ports       | ip             |
|------------|-------------|----------------|
| Management | Fa1/0       | 192.168.10.1   |
| Production |   Fa7/0     | 192.168.20.1   |
| Study      | Fa6/0       | 192.168.30.1   |
| Support    | Fa8/0       | 192.168.40.1   |
| Server     | Fa0/0       | 192.168.60.    |

Then we setup the server before finishing his config.
When server DHCP is done, we go to CLI interface from the router and put those command for each interfaces (exept the server interface)
```
enable 
configure terminal
interface 'name of the interface in question'
ip helper-address 'ip address of the DHCP server'
do write memory
```

Your network should be able now to communicate with the DHCP server and thus can  get the IPaddresses automatically assigned.

## Server part
All the server gonna be on a STATIC IP manually set

### DNS 192.168.60.253
Click on the server , set the default gateway. 
Set ip address on the interface : 192.168.60.253

Go to services , select DNS set it on add an URL name and it's IP addresses to the DNS record. 
This URL gonna be _www.cisco.com_ for this exercice.

### DHCP 192.168.60.254
Click on the server , set the default gateway. 
Set ip address on the interface : 192.168.60.254

Go to services, activate the DHCP service and configure each pool, by configuring the right network address, sub net, number of users and set the default gateway (IP-address of the router)  and the DNS and click Save.
When it's done go finish the setup of the router

### FTP 192.168.60.252
Click on the server , set the default gateway. 
Set ip address on the interface : 192.168.60.254 (this gonna be the access address of our server)

Go to services, activate the FTP service then we can set users and permission to access this storage.
To make the access easier than using ip adress we add a record to our DNS server and set _serv_ as url for the ftp server so we access the server using his url or his ip:










