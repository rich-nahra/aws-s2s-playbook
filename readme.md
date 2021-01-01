## aws-s2s-playbook

Configures Strongswan server to connect to an existing aws site-to-site vpn gateway. Strongswan runs as a virtual machine on your devbox or hypervisor if thats your jam. Once the tunnels are up you can add a route on your devbox to forward traffic to AWS over vpn. 

This playbook will read your AWS vpn connection information and configure strongswan IPSEC vpn including AZ failover.  

BPG routing protocol coming soon.  Using static routes for now...

Requirements

1. AWS cli with configured profile or AWS_XXX command line environment variables
1. Site to site vpn gateway and customer gateway in AWS
1. Ubuntu 20.04 virtual machine running
1. A user configured with password-less sudo and ssh public key

Running:

1. Copy `intentory.template.yml` to `inventory.yml` and update `inventory.yml` accordingly
1. Run playbook with `ansible-playbook -i inventory.yml playbook.yml` 
1. Add a route to your host machine
    ```bash
    # examples assuming strongswan is 192.168.1.2 and aws cidr is 10.0.0.0/16
    #linux
    sudo ip route add 10.0.0.0/16 via 192.168.1.2
    #macOS
    sudo route -n add -net 10.0.0.0/16 192.168.1.2
    ```




