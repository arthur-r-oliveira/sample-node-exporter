# sample-node-exporter

~~~
$ tree .
.
├── kustomization
│   └── base
│       ├── clusterrolebinding.yml
│       ├── daemonset.yml
│       ├── kustomization.yaml
│       ├── namespace.yml
│       ├── scc.yml
│       └── service-account.yml
└── README.md

2 directories, 7 files

$ oc apply -k kustomization/base/
namespace/monitoring configured
serviceaccount/node-exporter-sa configured
clusterrolebinding.rbac.authorization.k8s.io/system:openshift:scc:privileged configured
service/node-exporter created
daemonset.apps/node-exporter created

$ oc get pods -n monitoring
NAME                  READY   STATUS    RESTARTS   AGE
node-exporter-2hptm   1/1     Running   0          26s
 oc logs node-exporter-2hptm
ts=2024-04-01T10:23:52.277Z caller=node_exporter.go:192 level=info msg="Starting node_exporter" version="(version=1.7.0, branch=HEAD, revision=7333465abf9efba81876303bb57e6fadb946041b)"
ts=2024-04-01T10:23:52.277Z caller=node_exporter.go:193 level=info msg="Build context" build_context="(go=go1.21.4, platform=linux/amd64, user=root@35918982f6d8, date=20231112-23:53:35, tags=netgo osusergo static_build)"
ts=2024-04-01T10:23:52.278Z caller=diskstats_common.go:111 level=info collector=diskstats msg="Parsed flag --collector.diskstats.device-exclude" flag=^(ram|loop|fd|(h|s|v|xv)d[a-z]|nvme\d+n\d+p)\d+$
ts=2024-04-01T10:23:52.278Z caller=diskstats_linux.go:265 level=error collector=diskstats msg="Failed to open directory, disabling udev device properties" path=/run/udev/data
ts=2024-04-01T10:23:52.279Z caller=filesystem_common.go:94 level=warn collector=filesystem msg="--collector.filesystem.ignored-mount-points is DEPRECATED and will be removed in 2.0.0, use --collector.filesystem.mount-points-exclude"
ts=2024-04-01T10:23:52.279Z caller=filesystem_common.go:111 level=info collector=filesystem msg="Parsed flag --collector.filesystem.mount-points-exclude" flag=^/(dev|proc|sys|var/lib/docker/.+|var/lib/kubelet/pods/.+)($|/)
ts=2024-04-01T10:23:52.279Z caller=filesystem_common.go:113 level=info collector=filesystem msg="Parsed flag --collector.filesystem.fs-types-exclude" flag=^(autofs|binfmt_misc|bpf|cgroup2?|configfs|debugfs|devpts|devtmpfs|fusectl|hugetlbfs|iso9660|mqueue|nsfs|overlay|proc|procfs|pstore|rpc_pipefs|securityfs|selinuxfs|squashfs|sysfs|tracefs)$
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:110 level=info msg="Enabled collectors"
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=arp
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=bcache
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=bonding
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=btrfs
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=conntrack
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=cpu
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=cpufreq
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=diskstats
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=dmi
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=edac
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=entropy
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=fibrechannel
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=filefd
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=filesystem
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=infiniband
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=ipvs
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=loadavg
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=mdadm
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=meminfo
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=netclass
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=netdev
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=netstat
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=nfs
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=nfsd
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=nvme
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=os
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=powersupplyclass
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=pressure
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=rapl
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=schedstat
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=selinux
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=sockstat
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=softnet
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=stat
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=tapestats
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=textfile
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=thermal_zone
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=time
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=timex
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=udp_queues
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=uname
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=vmstat
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=xfs
ts=2024-04-01T10:23:52.279Z caller=node_exporter.go:117 level=info collector=zfs
ts=2024-04-01T10:23:52.280Z caller=tls_config.go:274 level=info msg="Listening on" address=[::]:9100
ts=2024-04-01T10:23:52.280Z caller=tls_config.go:277 level=info msg="TLS is disabled." http2=false address=[::]:9100
~~~
