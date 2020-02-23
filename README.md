# kubectl-execuser

## Overview

Exec as a specified user into a Kubernetes container. It has been tested on a kubernetes cluster v1.14.0.

It works by creating a pod on the same node as the container and mounting the docker socket into this container. The container runs the docker application which has access to the hosts containers and is able to use the exec command with the user flag.

## Install

Just clone the plugin script within a folder in your PATH:
```
git clone https://github.com/drodbar/kubectl-execuser/blob/master/kubectl-execuser ~//usr/local/bin/kubectl-execuser
```

## Usage

```
kubectl execuser $POD $COMMAND
```

If the command is not specified, falls back to the `sh` command.

**Flags**

| Name      | Shorthand | Default   | Usage                                                                     |
|-----------|-----------|---------- |---------------------------------------------------------------------------|
| remote-user      | -r        | root      | Username or UID.                                                          |
| container | -c        |           | Container name. If omitted, the first container in the pod will be chosen |
| name      | -o        | execuser | Name for new execuser pod to avoid `pods "execuser" already exists`     |                           | 

## Examples

Exec into first container in `example` pod with `sh` as user `root`.
```
kubectl execuser example
```

Exec into first container in `example` pod with `bash` as user `root`.
```
kubectl execuser example bash
```

Exec into first container in `example` pod with `bash` as user `admin`.
```
kubectl execuser -r admin example-pod bash
```

Exec into `second` container in `example` pod with `bash` as user `admin`.
```
kubectl execuser -c second -r admin example-pod bash
```
