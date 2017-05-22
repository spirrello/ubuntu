# ubuntu

This repo contains prereqs for standardizing Ubuntu deployments.

- install_prereqs
  - This playbook contains some basic packages required for Kubernetes, Contiv and Calico.  Is pretty generic for other use cases as well.

- install_sshkeys
  - Will deploy your sshkeys to the target servers.

- generate_kickstart
  - This playbook will generate a kickstart file for you.

- configure_bonding
  - This playbook will install the necessary package and load kernel modules to perform NIC bonding.  See below for an example of using this playbook:

  ansible-playbook -i environments/dev/inventory --limit at4d-lpk8sn03 configure_bonding.yml -u ubuntu -k -K --extra-vars '{"nic_1":"enp5s0f0", "nic_2":"enp5s0f1", "bond_nic":"bond0", "address":"10.27.9.123", "mask":"255.255.255.0", "network":"10.155.9.0", "broadcast":"10.155.9.255", "gateway":"10.155.9.1", "dns_search":"acme.dev acme.tech", "dns_servers":"10.27.137.151 10.27.137.152", "bond_mode":"0", "bond_miimon":"100"}'