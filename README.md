## OMC
---

Inspired by [omg tool](https://github.com/kxr/o-must-gather), with `omc` we want to be able to inspect a must-gather in the same way as we inspect a cluster with the oc command.

The `omc` tool does not simply parse the yaml file, it uses the official Kubernetes and OpenShift golang types to decode yaml file to their respective objects.

---
### Supported resources and flags

To date, the `omc get` command supports the following resources:

- Builds
- BuildConfigs
- ConfigMaps
- ClusterOperators
- ClusterVersion
- DaemonSets
- Deployments
- DeploymentConfigs
- Events
- Jobs
- Machines
- MachineConfigs
- MachineConfigPools
- MachineSets
- Nodes
- PersistentVolumes
- PersistentVolumeClaims
- Pods
- Projects
- ReplicationControllers
- ReplicaSets
- Secrets
- Services
- StorageClasses
- Routes

and the following flags:
- -A, --all-namespaces
- -n, --namespace
- -o, --output [ json | yaml | wide | jsonpath=... ]
- --show-labels

To date, the `omc logs` command supports the following resources:

- Pods

and the following flags:
- -p, --previous
- --all-containers

### Usage
Point it to an extracted must-gather:
```
$ omc use </path/to/must-gather/>
```
Use it like oc:
```
$ omc get clusterVersion
$ omc get clusterOperators
$ omc project openshift-ingress
$ omc get pods -o wide
```
#### Example
```  
$ omc use TEST/must-gather.local.1861325122907966446 -i 00000017

$ omc get mg                                                    
CURRENT   ID         PATH                                                                              NAMESPACE   
*         00000017   /Users/gmeghnag/Documents/GOLANG/omc/TEST/must-gather.local.1861325122907966446   default 

$ omc get nodes -o jsonpath="{range .items[*]}{.metadata.name}{'   '}{end}{'\n'}"
ip-10-0-130-107.eu-central-1.compute.internal   ip-10-0-138-105.eu-central-1.compute.internal   ip-10-0-170-202.eu-central-1.compute.internal   ip-10-0-191-105.eu-central-1.compute.internal   ip-10-0-192-202.eu-central-1.compute.internal   ip-10-0-216-17.eu-central-1.compute.internal
```
