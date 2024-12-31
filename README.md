# Agentkube Operator: Helm Charts

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/agentkube-operator)](https://artifacthub.io/packages/search?repo=agentkube-operator)

`AgentKube Operator` is a Kubernetes operator that enables seamless integration with the AgentKube platform for enhanced cluster management and monitoring capabilities.

For detailed information about AgentKube and its features, visit our [documentation](https://docs.agentkube.com).

## Prerequisites

- Kubernetes 1.16+
- Helm 3.x
- A valid AgentKube API key (Generate from [AgentKube Dashboard](https://dashboard.agentkube.com/settings/manage/api-keys))
- Kubectl access to your cluster

## Installation

1. Add the AgentKube Helm repository:
   ```bash
   helm repo add agentkube https://agentkube.github.io/helm-charts
   helm repo update
   ```

2. Install the operator:
   ```bash
   helm install agentkube-operator agentkube/agentkube-operator-charts \
     -n agentkube-operator-system \
     --create-namespace
   ```

### Configuration

The following table lists the configurable parameters of the AgentKube Operator chart and their default values:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `manager.serverEndpoint` | AgentKube Server Endpoint | `https://api.agentkube.com` |
| `manager.apikey` | AgentKube API Key | `""` |
| `manager.clusterName` | Cluster Name | `local_cluster` |
| `manager.readonly` | Read-Only Mode | `true` |
| `replicaCount` | Number of operator replicas | `1` |
| `image.repository` | Operator image repository | `agentkube/agentkube-operator` |
| `image.tag` | Operator image tag | `v0.2.0` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |

### Example Values File

```yaml
manager:
  serverEndpoint: https://api.agentkube.com
  apikey: your_api_key_here  # Get from https://dashboard.agentkube.com/settings/manage/api-keys
  clusterName: prod-cluster
  readonly: false
```

## Usage

After installation, the operator will automatically register your cluster with the AgentKube platform. You can access the metrics and management features through your [AgentKube Dashboard](https://dashboard.agentkube.com).

For local development and testing:
```bash
kubectl port-forward -n agentkube-operator-system svc/agentkube-operator-controller 8082:8082
```

## Contributing

We welcome contributions to the AgentKube Operator Helm Charts! Here's how you can contribute:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow the [Helm best practices](https://helm.sh/docs/chart_best_practices/) when modifying charts
- Update documentation as needed
- Add/update tests for new features
- Ensure backwards compatibility or document breaking changes
- Include relevant issue numbers in PRs
- Keep changes focused and atomic

## Support

For support, please:
1. Check the [documentation](https://docs.agentkube.com)
2. Open an issue in this repository
3. Contact AgentKube support through official channels

## License

This project is licensed under the Apache License - see the [LICENSE](/LICENSE) file for details.