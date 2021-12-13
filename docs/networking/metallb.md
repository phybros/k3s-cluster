# MetalLB

Luckily, my usage of MetalLB is super basic. `Service` objects of type `LoadBalancer` are given an IP address from the local network router using ARP.

The relevant piece of config is <https://github.com/phybros/k3s-cluster/blob/main/cluster/core/metallb-system/helm-release.yaml#L18-L24>

The variable `METALLB_LB_RANGE` is set in <https://github.com/phybros/k3s-cluster/blob/main/cluster/base/cluster-settings.yaml#L14>
