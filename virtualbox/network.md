# Network configuration

## Host only network

Host only network can be used alongside with NAT-adapter to enable communication between host machine and virtual machine.

### Virtual Box configuration
1. Create HostOnly network in File -> Host Network Manager
  - Select configure adapter automatically
  - Enable DHCP server.
  - Open DHCP Server tab and choose one IP address between the Lower and Upper Address Bounds. For example if lower address bound is 192.168.93.3 and upper 192.168.93.254, you can choose to use `192.168.93.56`.

2. Add second network adapter (HOST ONLY) in VirtualBox settings.
  - Make sure that the host-only network created in first step is used.

### Ubuntu server configuration
3. Start Ubuntu Server.
4. Find the name of the host only adapter with `ifconfig -a` (e.g. `enp0s8`)
5. Create following configuration file in `etc/netplan/01-netcfg.yaml`. Note that the adapter name `enp0s8` and the ip address `192.168.93.56` are figured out in steps 1 and 4, hence **copy-pasting the following snippet won't probably work directly**.

``` yaml
network:
  version: 1
  renderer: networkd
  ethernets:
    enp0s8:
      addresses:
        - 192.168.93.56/24
```

  - Apply configuration changes with `sudo netplan apply`

# Configuring ssh using port forwarding and NAT

In *VM settings -> Network -> NAT adapter -> Advanced -> Port forwarding* add following settings

|Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
|-----| ---------| --------| ------|-|-|
|ssh  | TCP| | 2222 | | 22

VM can be reached with `ssh username@localhost -p 2222`.
