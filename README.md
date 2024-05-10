# ansible_masterclass

## csr1000v ssh config

config t
Enter configuration commands, one per line.  End with CNTL/Z.

csr1000v(config)#username admin privilege 15 secret cisco
csr1000v(config)#crypto key generate rsa modulus 2048 general-keys
csr1000v(config)#line vty 0 4
csr1000v(config-line)#login local
csr1000v(config-line)#transport input ssh

csr1000v(config-line)#^Z
csr1000v#copy running-config startup-config
