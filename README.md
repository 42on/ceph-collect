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

Allow the tool to run for about 5 minutes to gather all the required information.

## Output
After the tool finishes a tarball will be placed in */tmp* containing all the information.

Send this tarball to [info@42on.com](mailto:info@42on.com)
