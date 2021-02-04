# derpz4000
kubernetes with bgp lab

My challenge here was to create a quick k8s single-node cluster with BGP and Calico, with only existing equipment and a few yaml files.
All external equipment, network cidrs are all completely aribitrary.  Your results may vary.  

Requirements: 

* docker-compose
* RKE binary
* ansible

ERX1 is an external edgerouter X.  Rocket is a single vm-node.  
This could be improved ... the STATIC-TO-BGP route-map is misleading, it just filters what networks one would like to accept/advertise.

Every new node-- like worker nodes in k8s-- would need to be added to the ansible file.  This could be a loop or playbook.  

There's a better option to bring a top-of-rack (TOR) BGP session closer to the VM, using perhaps FRrouting in a docker container or other k8s cluster/pods.

Included some information around using FRRouting as a docker container TOR device.  It sits between the guest node-vms in the cluster, and the ERX1 equipment in the lab environment.  This frr-TOR-bgp device is configured as a route-reflector.  Docker-compose file for the container and a sample config also included.

Included "daemons" which is one of the config files for FRR that now lives on the Docker host under /usr/local/etc ... for purposes of this lab, only vtysh_enabl and bgpd are enabled, that is the only difference from the default install configuration.
