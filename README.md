# Cluster

A repo storing resource files and ansible playbooks for my k3s cluster.

## How to use

**YAML**

For easier identification from the filenames, the rule I name the files are as below : 

`.yaml` files are kubernetes resources definition files, use by `kubectl create -f [filename].yaml`

`.yml` files are helm chart value files, use by `helm install [name] [chart-repo/chart-name] (-n [namespace]) -f [filename].yml`

**Deploy mesh network**

Conditions: Ubuntu system, Ansible installed already.

Modify the `hosts.ini` file:

```ini
[mesh]
master.your.host.name  vpn_ip=192.168.1.1  site_net=A
oracle-1.your.host.name  vpn_ip=192.168.1.2  site_net=B
oracle-2.your.host.name  vpn_ip=192.168.1.3  site_net=B
civo-1.your.host.name  vpn_ip=192.168.1.4  site_net=C

[all:vars]
ListenPort=51800
```

Run:

`ansible-playbook ./up.mesh.1.yml`

To **disable** the services from running at startup, cd to the `./mesh` folder:

`ansible mesh -m systemd -a "name=wg-quick@mesh.1 enabled=no" `

## Credits

* [wireguard_playbook](https://github.com/turbotankist/wireguard_playbook)
