# Sysctl not loaded at boot on Alpine

I had the problem on Alpine 3.20. 

## Problem description

I want to activate ip forwarding and persist configuration (after reboot).  
For this, i create sysctl file into directory `/etc/sysctl.d/*.conf`.  
Bellow a example of configuration

```sh
net.ipv4.ip_forward=1
```

To load this configuration, use `sysctl -p /etc/sysctl.d/ip_forward.conf`.  
We can check this new configuration with command `sysctl net.ipv4.ip_forward` and output shoud be `net.ipv4.ip_forward = 1`.  

But, if the system reboot, the configuration files into directory `/etc/sysctl.d/*.conf` will not be applied (what should be the default behavior).  

## Problem solving

If these config files are not loaded at startup, first check if the service sysctl is well loaded at boot. 
Use one of the command `rc-update --all` or `rc-update -v show` for this.  
The service sysctl is not listed, It's necessary to add it with the command `rc-update add sysctl boot`
Now, sysctl configuration files are persisted. 

