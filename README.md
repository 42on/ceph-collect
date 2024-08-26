# Ceph Collect
The *ceph-collect* tool is used by [42on](http://www.42on.com/) to gather diagnostic information from a Ceph cluster.

The output from the tool is used to assist customers in case of questions, support or emergency situations.

The tarball the tool creates contains vital information for our engineers to support our customers.

This tool does **NOT** collect any user (object) data contents nor authentication credentials from a Ceph cluster.

# Usage
The first step is to download the tool from [Github](https://github.com/42on/ceph-collect).

You can either clone the Git repository or download just the tool:

## Git clone
```
git clone https://github.com/42on/ceph-collect
cd ceph-collect
```

## Fetch from Github
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

## Where to run
This tool should be run on a machine which is able to connect to the Ceph cluster and has the *client.admin* keyring.

In most of the situations the *monitors* are the right location to run this tool.

## Running
When the requirements are met, simply run the *ceph-collect* tool:
The ceph-collect script is compatible with python versions 2 and 3. Ceph itself is not compatible with both versions.

### Octopus and newer:

``./ceph-collect``

### Nautilus and older:

``python2 ./ceph-collect``

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
INFO:root:Outputted Ceph information to /tmp/ceph-collect_20160729_150304.tar.gz
DEBUG:root:Cleaning up temporary directory: /tmp/tmpMpFk3n
root@mon01:~#
```
### Gathering Device Health information
By default  ``ceph-collect`` doesn't collect the device's health information. Use ``--device-health-metrics`` to enable it.

``ceph-collect --device-health-metrics``

### One-liner
If you want to run this tool without downloading it, you can run it directly using this one-liner:

``curl -SL https://raw.githubusercontent.com/42on/ceph-collect/master/ceph-collect|python``

It will not save the tool on disk, it just runs the Python code and saves the output in */tmp*.


## Output
After the tool finishes a tarball will be placed in */tmp* containing all the information.

This tarball should be just a few kilobytes in size.

For example: */tmp/ceph-collect_20160729_150304.tar.gz*

Send this tarball to [info@42on.com](mailto:info@42on.com) for analyses.

### Auto upload
If you want to upload the ceph-collect to 42on, use the ``--upload`` argument.

# License
This tool was written by [42on](http://www.42on.com/) to help Ceph customers quickly.

The tool is free to use for all other purposes. It's licensed GPLv2, so please send changes back to us!
