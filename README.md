<div align="center">

<img src="https://raw.githubusercontent.com/phybros/k3s-cluster/main/docs/logo.png" align="center" width="144px" height="144px"/>

### My home Kubernetes cluster :sailboat:

_... managed with Flux and Renovate_ :robot:

</div>

<br/>

<div align="center">

[![discord](https://img.shields.io/discord/673534664354430999?label=discord&logo=discord&logoColor=white)](https://discord.gg/k8s-at-home)
[![k3s](https://img.shields.io/badge/k3s-v1.31-brightgreen?logo=kubernetes&logoColor=white)](https://k3s.io/)
[![renovate](https://img.shields.io/badge/renovate-enabled-brightgreen?logo=renovatebot&logoColor=white)](https://github.com/renovatebot/renovate)
[![lines](https://tokei.rs/b1/github/phybros/k3s-cluster)](https://github.com/phybros/k3s-cluster)

</div>

---

## :book:&nbsp; Overview

This is home to my personal Kubernetes cluster. [Flux](https://github.com/fluxcd/flux2) watches this Git repository and makes the changes to my cluster based on the manifests in the [cluster](./cluster/) directory. [Renovate](https://github.com/renovatebot/renovate) also watches this Git repository and creates pull requests when it finds updates to Docker images, Helm charts, and other dependencies.

## :handshake:&nbsp; Community

Thanks to all the people who donate their time to the [Kubernetes @Home](https://github.com/k8s-at-home/) community.
