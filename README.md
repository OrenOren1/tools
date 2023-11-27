
# Tools Repository

Welcome to the `tools` repository! This repository contains two main Helm charts:

1. `self-hosted-github-runners`
2. `tailscale-subnet-router`

Each folder contains a Helm chart for deploying and managing specific services. Below you'll find the configuration details for each.

## Self-Hosted GitHub Runners

The `self-hosted-github-runners` directory contains a Helm chart for deploying self-hosted runners for GitHub Actions in your Kubernetes cluster. 

### Configuration

The following table lists the configurable parameters for the `self-hosted-github-runners` chart and their default values.

| Parameter                  | Description                           | Default          |
|----------------------------|---------------------------------------|------------------|
| `replicaCount`             | Number of runner replicas to deploy   | `1`              |
| `githubToken`              | GitHub token for runner authentication | `""`             |
| `runner.image`             | The Docker image for the runner       | `my-runner-image`|
| `runner.tag`               | The Docker image tag                  | `latest`         |
| ...                        | ...                                   | ...              |

### Installation

To install the chart with the release name `my-release`:

```bash
helm install my-release ./self-hosted-github-runners
```

### Additional Information

- Make sure to provide a valid GitHub token with appropriate permissions.
- You can customize other values by editing the `values.yaml` file.

## Tailscale Subnet Router

The `tailscale-subnet-router` directory contains a Helm chart for setting up a Tailscale subnet router on your Kubernetes cluster.

### Configuration

The following table lists the configurable parameters for the `tailscale-subnet-router` chart and their default values.

| Parameter                  | Description                          | Default          |
|----------------------------|--------------------------------------|------------------|
| `tailscale.authKey`        | Tailscale authentication key         | `""`             |
| `network.cidr`             | CIDR for the Tailscale network       | `10.0.0.0/16`    |
| `image.repository`         | The image repository for the router  | `tailscale/tailscale` |
| `image.tag`                | The image tag                        | `latest`         |
| ...                        | ...                                  | ...              |

### Installation

To install the chart with the release name `my-tailscale`:

```bash
helm install my-tailscale ./tailscale-subnet-router
```

### Additional Information

- You must provide a valid Tailscale authentication key for the subnet router to function correctly.
- Modify the `values.yaml` file for additional customizations.

---

## Contributing

Contributions to improve the Helm charts or any other aspects of this repository are welcome. Please feel free to submit issues and pull requests.

---
