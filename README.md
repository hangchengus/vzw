#WDS CSAR


## Prerequisites

Before uploading CSAR, one must create project, user, image, OAM
network, Internal network,, Database network, Signaling network, Internet network and flavor:

```sh
$ openstack project create \
    --description "WDS" \
    WDS
```

```sh
$ openstack quota set --server-groups -1 WDS
```

```sh
$ openstack quota set --server-group-members -1 WDS
```

```sh
$ openstack user create \
    --project WDS \
    --password nokia123 \
    wds
```

```sh
$ openstack role add \
    --project WDS \
    --user wds \
    admin
```

```sh
$ openstack image create \
    --disk-format qcow2 \
    --container-format bare \
    --file ../images/nokia-rhel-server-7.6-x86_64-kvm-base \
    redhat-76-base
```

```sh
$ openstack network create \
    --project WDS \
    --no-share \
    --internal \
    --provider-network-type vlan \
    --provider-physical-network physnet0 \
    --provider-segment 2099 \
    WDS_OAM
```

```sh
$ openstack subnet create \
    --project  WDS \
    --network WDS_OAM \
    --subnet-range 2a00:8a00:2000:132:22::/64 \
    --gateway 2a00:8a00:2000:132:22::1 --ip-version 6 \
    --allocation-pool start=2a00:8a00:2000:132:22::3,end=2a00:8a00:2000:132:220::500 \
    WDS_OAM_SUBNET
```
```sh
$ openstack network create \
    --project WDS \
    --no-share \
    --internal \
    --provider-network-type vlan \
    WDS_INTERNAL
```

```sh
$ openstack subnet create \
    --project WDS \
    --network WDS_INTERNAL \
#    --subnet-range 2a00:8a00:2000:132:22::/126 \ <== update here
#    --gateway 2a00:8a00:2000:132:22::1 --ip-version 6 \ <== update here
#    --allocation-pool start=2a00:8a00:2000:132:22::3,end=2a00:8a00:2000:132:220::500 \ <== update here
    WDS_INTERNAL_SUBNET
```
```sh
$ openstack network create \
    --project WDS \
    --no-share \
    --internal \
    --provider-network-type vlan \
    WDS_DATABASE
```

```sh
$ openstack subnet create \
    --project WDS \
    --network WDS_DATABSE \
#    --subnet-range 2a00:8a00:2000:132:22::/126 \ <== update here
#    --gateway 2a00:8a00:2000:132:22::1 --ip-version 6 \ <== update here
#    --allocation-pool start=2a00:8a00:2000:132:22::3,end=2a00:8a00:2000:132:220::500 \ <== update here
    WDS_DATABASE_SUBNET
```

```sh
$ openstack network create \
    --project WDS \
    --no-share \
    --internal \
    --provider-network-type vlan \
    WDS_SIGNAL
```

```sh
$ openstack subnet create \
    --project WDS \
    --network WDS_SIGNAL \
#    --subnet-range 2a00:8a00:2000:132:22::/126 \ <== update here
#    --gateway 2a00:8a00:2000:132:22::1 --ip-version 6 \ <== update here
#    --allocation-pool start=2a00:8a00:2000:132:22::3,end=2a00:8a00:2000:132:220::500 \ <== update here
    WDS_SIGNAL_SUBNET
```
```sh
$ openstack network create \
    --project WDS \
    --no-share \
    --internal \
    --provider-network-type vlan \
    WDS_INTERNET
```

```sh
$ openstack subnet create \
    --project WDS \
    --network WDS_SIGNAL \
#    --subnet-range 2a00:8a00:2000:132:22::/126 \ <== update here
#    --gateway 2a00:8a00:2000:132:22::1 --ip-version 6 \ <== update here
#    --allocation-pool start=2a00:8a00:2000:132:22::3,end=2a00:8a00:2000:132:220::500 \ <== update here
    WDS_INTERNET_SUBNET
```
```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 8 \
    wds-fe
```

```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 8 \
    wds-be
```

```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 8 \
    wds-oam
```

```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 2 \
    wds-ops
```

```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 8 \
    wds-db
```

```sh
$ openstack flavor create \
    --ram 8192 \
    --disk 50 \
    --vcpu 8 \
    wds-conf
```


