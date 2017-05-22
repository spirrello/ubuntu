# ubuntu

This repo contains prereqs for standardizing Ubuntu deployments.

- install_prereqs
  - This playbook contains some basic packages required for Kubernetes, Contiv and Calico.  Is pretty generic for other use cases as well.

- install_sshkeys
  - Will deploy your sshkeys to the target servers.

- configure_bonding
  - This playbook will install the necessary package and load kernel modules to perform NIC bonding.  See below for an example of using this playbook:
  - bond_mode
    - This setting will determine which mode for bonding NICs.  In this examlple we use mode 0 for a round robin approach for transmitting data on the wire.
  - bond_miimon
    - Frequency of link monoitoring in ms.  Kernel.org recommends a value of 100.


  ansible-playbook -i environments/dev/inventory --limit at4d-lpk8sn03 configure_bonding.yml -u ubuntu -k -K --extra-vars '{"nic_1":"enp5s0f0", "nic_2":"enp5s0f1", "bond_nic":"bond0", "address":"10.27.9.123", "mask":"255.255.255.0", "network":"10.155.9.0", "broadcast":"10.155.9.255", "gateway":"10.155.9.1", "dns_search":"acme.dev acme.tech", "dns_servers":"10.27.137.151 10.27.137.152", "bond_mode":"0", "bond_miimon":"100"}'