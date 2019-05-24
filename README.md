# kubectl-exec-user

## Overview

Exec as a specified user into a Kubernetes container.

This works by creating a pod on the same node as the container and mounting the docker socket into this container. The container runs the docker application which has access to the hosts containers and is able to use the exec command with the user flag.

## Install

Just clone the plugin within the plugins folder with:
```
git clone https://github.com/drodbar/kubectl-exec-user.git ~/.kube/plugins/exec-user
```

## Usage

```
kubectl plugin exec-user $POD $COMMAND
```

If the command is not specified, falls back to the `sh` command.

**Flags**

| Name      | Shorthand | Default   | Usage                                                                     |
|-----------|-----------|---------- |---------------------------------------------------------------------------|
| remote-user      | -r        | root      | Username or UID.                                                          |
| container | -c        |           | Container name. If omitted, the first container in the pod will be chosen |
| name      | -o        | exec-user | Name for new exec-user pod to avoid `pods "exec-user" already exists`     |                           | 

## Examples

Exec into first container in `example` pod with `sh` as user `root`.
```
kubectl plugin exec-user example
```

Exec into first container in `example` pod with `bash` as user `root`.
```
kubectl plugin exec-user example bash
```

Exec into first container in `example` pod with `bash` as user `admin`.
```
kubectl plugin exec-user -r admin example-pod bash
```

Exec into `second` container in `example` pod with `bash` as user `admin`.
```
kubectl plugin exec-user -c second -r admin example-pod bash
```
