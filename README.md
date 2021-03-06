# ZFS Freight Service

[![Build Status](https://travis-ci.org/BigVikingGames/zfs-freight-service.svg?branch=master)](https://travis-ci.org/BigVikingGames/zfs-freight-service)

__ZFS Freight Service__ is a Docker volume plugin that allows you to create and mount persistent ZFS volumes. It is
based heavily off [CWSpear/local-persist](https://github.com/CWSpear/local-persist) and currently
only supports single nodes. Basic implementation of the volume API should be complete. The eventual goal is to provide a robust ZFS-based volume manager for Docker clusters.

It's worth noting that ZFS slices created by this plugin are __not destroyed__ when a volume is removed. This also means that you will get an error if you attempt to create the same named volume again.

## Install

```
$ make binary
$ export FREIGHT_ZPOOL=your-pool
$ sudo -E ./bin/zfs-freight &
```

## Configuration

```
# defaults
FREIGHT_LISTEN=:2379
FREIGHT_ZPOOL=tank
```

## Docker Usage

```
# create a simple volume
$ docker volume create -d zfs-freight --name test-volume

# create a volume with custom zfs options
$ docker volume create -d zfs-freight --name custom-volume -o compression=on -o atime=off

# mounting your volume
$ docker run -it -v custom-volume:/data ubuntu:14.04 bash

```

## Development

```
$ vagrant up
$ vagrant ssh
$ cd /vagrant
$ make run
```
