# Home Cluster

This repo is where the state of my home k3s cluster is declared. As changes are pushed to the repo, [Flux](https://github.com/fluxcd/flux2) applies those changes to the running cluster. All of the configuration that Flux cares about is in the `cluster/` directory of the repo.

This repo was created from the [k8s-at-home/template-cluster-k3s](https://github.com/k8s-at-home/template-cluster-k3s) template repo which can get you up and running with a similar setup in no time.

Take your questions to the [Kubernetes @Home Discord](https://discord.gg/k8s-at-home)! It's full of awesome people, and a wealth of knowledge.

## Components

- [Flux](https://fluxcd.io/docs/): Watches this repo and applies changes to the cluster.
- [MetalLB](https://metallb.universe.tf/): Implementation of `LoadBalancer` for bare metal Kubernetes clusters, using standard routing protocols (give any `Service` an IP on your network via ARP!).
- [Traefik](https://doc.traefik.io/traefik/providers/kubernetes-ingress/): My preferred ingress controller to expose traffic to pods.
- [cert-manager](https://cert-manager.io/docs/): Configured to create TLS certs for all ingress services automatically using LetsEncrypt.
- [Mozilla SOPS](https://toolkit.fluxcd.io/guides/mozilla-sops/): Encrypts secrets which is safe to store - even to a public repository.
- [rook-ceph](https://rook.io/): Provides persistent volumes, allowing any application to consume RBD block storage.
- [benji](https://benji-backup.me/index.html): Automated backups of rook-ceph PVCs, management of backup retention, and restoration of backups to new PVCs.
- And lots more!

Check the site nav for more info about the setup of some of these.

## Repository structure

The Git repository contains the following directories under `cluster` and are ordered below by how Flux will apply them.

- **base** directory is the entrypoint to Flux
- **crds** directory contains custom resource definitions (CRDs) that need to exist globally in your cluster before anything else exists
- **core** directory (depends on **crds**) are important infrastructure applications (grouped by namespace) that should never be pruned by Flux
- **apps** directory (depends on **core**) is where your common applications (grouped by namespace) could be placed, Flux will prune resources here if they are not tracked by Git anymore

```
./cluster
├── ./apps
├── ./base
├── ./core
└── ./crds
```
