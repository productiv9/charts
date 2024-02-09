# Ghost Helm Chart

This repository hosts the Helm chart for deploying [Ghost](https://ghost.org/) on Kubernetes clusters. Ghost is a powerful open-source publishing platform designed for professional blogging.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+
- Persistent Volume (PV) provisioner support in the underlying infrastructure, if persistence is enabled

## Installation

To add this Helm repository and install the Ghost chart with the release name `my-ghost`, run:

```shell
helm repo add ghost https://productiv9.github.io/charts
helm repo update
helm install my-ghost ghost/ghost --version 0.1.0 -f values.yaml
```
