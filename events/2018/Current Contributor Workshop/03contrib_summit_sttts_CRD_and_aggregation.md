# CRDs and Aggregation

Focus is extension mechanisms and missing features.

## Aggregation

API is stable since 1.10.  There is a lack of tools and library
support.

GSoC project on shared etcd storage.

## Custom Resources

For 1.11 multiple alpha features planned (see slides for list).
Pruning feature is a blocker for GA.  Subresources moving to beta
from 1.10 alpha, and discussion of custom subresources.

CRDs are a json blob, pruning of which leads to a change in semantics
and needs solidified for CRDs to go GA/stable.  The new implemetation
is more normal for golang json handling, and the implementation
also makes it easier to indicate a resource is a default.  If there
are any users who require persisting of values in the json blob
which would otherwise be pruned, the use case needs discussed.
There is complexity around balancing silently dropping (golang json
parsing bug?), giving validation error, and pruning values in json blobs.

Versioning has been discussed since the beginning.  In the past you
couldn't have two versions of the same resource.  You had to delete
the CRD and all its data and then reimport the new one.  A simpler
"NoConversion" versioning might land in 1.11, and a "Declarative
Conversions" system could come in 1.12 with a goal of keeping it
simple, universal, and able to go forward and backward.  (see
slides for sketched example)  A webhook has been discussed, but is
complicated.  Latest versioning design proposal is [k/community PR #2026](https://github.com/kubernetes/community/pull/2026)

CRD's versus aggregated API servers:  today recommendation is to start with
CRDs, but there's not a clear migration path.

Resource quotas: PoC PR is roughly working.  It's doable, we know how, just
needs some time.  May make 1.11.

Validation field:  will it be required?  Voices in room saying yes it
should be.  Multiple folks using validations.

Namespaced CRDs: There was discussion in Austin at 2017 KubeCon NA, but it
hasn't progressed.  It is complicated.
