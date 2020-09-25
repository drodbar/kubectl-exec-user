# kubectl-execuser

## Overview

Exec as a specified user into a Kubernetes container. It has been tested on a kubernetes cluster versions v1.14.x and 1.16.10

It works by creating a pod on the same node as the container and mounting the docker socket into this container. The container runs the docker application which has access to the hosts containers and is able to use the exec command with the user flag.

## Install

Just clone the plugin script within a folder in your PATH:
```
wget https://raw.githubusercontent.com/drodbar/kubectl-execuser/master/kubectl-execuser -O /usr/local/bin/kubectl-execuser
chmod +x /usr/local/bin/kubectl-execuser
```

To check correct installation run:
```
kubectl plugin list
```
if the binary path appears in the output, you are ready to go!

## Usage

```
kubectl execuser [(-n|--namespace) $NAMESPACE][(-s|--shell) $SHELL][-c|--container-index $CONT_IDX][(-u|--username)] [(-h|--help)][(-v|--verbose)][(-d|--debug)]  $POD
```

The pod name is the only mandatory argument, and it can be placed anywhere.

**Flags**

| Name            | shortopt  | longopt           | Default  | Usage                                                         |
|-----------------|-----------|-------------------|----------|---------------------------------------------------------------|
| username        | -u        | --username        | root     | Username or UID                                               |
| namespace       | -n        | --namespace       | default  | Namespace. It will default to current, if any, or 'default'   |
| container-index | -c        | --container-index | 0        | Container index                                               |
| shell           | -s        | --shell           | sh       | Shell to run                                                  |
| debug           | -d        | --debug           | .        | Debug mode                                                    |
| verbose         | -v        | --verbose         | .        | Verbose mode                                                  |
| help            | -h        | --help            | .        | Show help                                                     |

## Examples

Exec into first container in `example` pod with `sh` as user `root`.
```
kubectl execuser example
```

Exec into first container in `example` pod with a `bash` shell as user `root`.
```
kubectl execuser example -s bash
```

Exec into first container in `example` pod with `bash` as user `admin`.
```
kubectl execuser -u admin example-pod -s bash
```

Exec into `` container in `example` pod with a `bash` shell and user `admin`.
```
kubectl execuser -c 1 -u admin example-pod -s bash
```
