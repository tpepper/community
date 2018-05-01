# What's Next in Networking?

This session is not declaring what's being implemented next, but rather
laying out the problems that loom.

## Specific items coming near term

* kube-proxy with
  [IPVS](https://github.com/kubernetes/community/pull/1978): beta
  now.  IPVS requires kernel module, but that exists and is done,
  stable, and complete on the kernel side.

* CoreDNS replacing kube-dns: beta now

* [ready++](https://github.com/kubernetes/community/blob/master/keps/sig-network/0007-pod-ready%2B%2B.md)
  project: not quite alpha (maybe v1.11).  Allows external networking
  to be a factor when doing a rolling update.  Say your load-balancer
  takes 5-10 seconds to program, when you bring up new pod and take
  down old pod the load balancer has lost old backends but hasn't
  yet added new backends.  The external dependency like this becomes
  a gating pod decorator.


## Ingress

Originally designed to be lowest-common-denominator API and is
limited by cloud-providers.  This is really limiting for users,
especially compared to modern software L7 proxies.

Survey shows everybody wants ingress to be portable and everybody
uses a non-portable feature.

Ideas for revamping are floating around.  One is to up-level the baseline
API, which could mean deprecating support for less capable cloud providers.
Another is something more like OpenShift routes model.  Heptio is
prototypeing something here.

Istio is maturing rapidly and its new APIs are nice, but it is a
little green still.  Given that plus  istio is not part of kubernetes,
it's unlikely near term to become a default or required part of a
k8s deployment.  The general ideas around istio style service mesh
could be more native in k8s.

## Topology and Node-local services

There is user demand for node-local services.  Unclear the right
architecture/implementation.

## Multi-network

A pod can be in multiple networks at once.  You might have different
quality of service on different networks (eg: fast/expensive,
slower/cheaper), or different connectivity (eg: the rack-internal
network).

Network related interfaces in k8s today do not allow multiple pod IPs or
dynamic configuration.

Need to not reinvent the same problems.  Kubernetes is about apps.  Network
topology details are about infrastructure.

PoC CRD is underway.

Question: Would this PoC help if virtual-kubelets were used to span
cloud providers? Spanning latency domains in networks is also
complicated.  Many parts of k8s are chatty, assuming a cluster
internal low-latency connectivity.

## Net plugins vs. device plugins

Say you have a GPU that is also an infiniband device.  The plugin
APIs are not coordinated today.  To use this combo device you need
your pod to land on a node with the GPU that is also the intended
infiniband device.  The general shape of the problem's reasonable
described, but forward path looks like deep changes.  This spans
networking and resource management SIGs/WGs.  Conversation may feel like a
cycle, but @thockin feels it is a spiral that is slowly converging and he
has a doc he can share covering the evolving thinking.

## Net plugins, gRPC, Services

Tighter coupling between net plugins and kube-proxy could be useful.  Could
components be daemonsets to combine for easy of deployment?

## IPv6

Support for single stack (IPv6 only) is in beta now, but not support yet for
dual-stack (IPv4 and IPv6).  A lot of work remains.  Mostly understood but
needs time and work. [Dual stack feature tracking](https://github.com/kubernetes/features/issues/563)

## Services v3

Services and endpoints grew organically and the result is mostly a grab-bag
of features.  A next iteration could be segmenting of the "core" API group.

Could "endpoints" be "endpoint?  Split grouping selector construct
from all the things that go into the services.  There is a set of hard
features that are poorly implemented and probably deserve to be end of
life'd for simplicity, reliability, performance reasons.

## DNS Reboot

Kubernetes abuses DNS and has a messed up DNS schema.  We have to
care about compatibility so changing this is hard.  Could there be
something like a two year phasing in of a new schema where an app
developer can choose which one they use.  The schema issues are
things like it's too easy to make a "com" and "google" and then
your search path is messed up, referring to some k8s service.  Of
course it wont "work" because of SSL.  But you easily get breakage.

Could a new DNS RFC be drafted to make a more enlightened DNS system that
considers the use cases of cloud native and kubernetes clusters.

Could UDP used for node-local lookups, and non-node-local leverage gRPC?

## Performance and Scalability

In general programmability is getting better.

iptables is krufty.  nftables implementation should be better.

ebpf implementation (eg; Cilium) has potential

## External DNS and Ingress

[External DNS
project](https://github.com/kubernetes-incubator/external-dns) synchronizes k8s services into external DNS.  This
project has been an incubator and needs to figure out where it goes next.
Widely used in production.  It might not be a core kubernetes project,
could use a KEP to decide where it goes.

## API flux

Question around adding new APIs versus extending existing, and do
we deprecate old ones?  No we can't just turn old things off and
stop supporting them.  No plans for an API v2.  It takes enterprise
users years to move to new things.
