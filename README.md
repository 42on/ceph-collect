# Ceph Collect
The 'ceph-collect' tool is used by 42on to gather diagnostic information from a Ceph cluster.

The output from the tool is used to assist customers in case of questions, support or emergency situations.

# Usage
The first step is to download the tool from [Github](https://github.com/42on/ceph-collect).

You can either clone the Git repository or download just the tool:

## Git clone
```
git clone https://github.com/42on/ceph-collect
cd ceph-collect
```


```
curl -SL -o ceph-collect https://raw.githubusercontent.com/42on/ceph-collect/master/ceph-collect
chmod +x ceph-collect
```

## Requirements
To run the tool, the following requirements need to be met:
* Python 2.7 or higher
* python-rados, ceph and ceph-common RPM or DEB installed
* client.admin keyring present in /etc/ceph
* /etc/ceph/ceph.conf configured to connect to Ceph cluster

You can test this by running:

``ceph health``

This should output either *HEALTH_OK*, *HEALTH_WARN* or *HEALTH_ERR*.

## Running
When the requirements are met, simply run the *ceph-collect* tool:

``./ceph-collect``

Usually the tool finishes within a few seconds, but if a Ceph cluster is experiencing issues it might take up to 5 minutes.

The output it will print while running:


```
root@mon01:~# ./ceph-collect --debug
DEBUG:root:Using Ceph configuration file: /etc/ceph/ceph.conf
DEBUG:root:Setting client_mount_timeout to: 10
DEBUG:root:Connecting to Ceph cluster
DEBUG:root:Using temporary directory: /tmp/tmpMpFk3n
INFO:root:Gathering overall Ceph information
INFO:root:Gathering Health information
INFO:root:Gathering MON information
INFO:root:Gathering OSD information
INFO:root:Gathering PG information
INFO:root:Gathering MDS information
INFO:root:Outputted Ceph information to /tmp/ceph-collect_20160729_150304.tar
DEBUG:root:Cleaning up temporary directory: /tmp/tmpMpFk3n
root@mon01:~#
```


## Output
After the tool finishes a tarball will be placed in */tmp* containing all the information.

Send this tarball to [info@42on.com](mailto:info@42on.com) for analyses.
