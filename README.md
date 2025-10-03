# MariaDB Helm Chart

A Helm chart for deploying MariaDB 10.4 on Kubernetes.

## Introduction

This chart bootstraps a MariaDB deployment on a Kubernetes cluster using the Helm package manager.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- PV provisioner support in the underlying infrastructure (if persistence is enabled)

## Installing the Chart

To install the chart with the release name `my-mariadb`:

```bash
helm install my-mariadb .
```

## Upgrading the Chart

To upgrade an existing release to a new version:

```bash
helm upgrade my-mariadb .
```

To upgrade with specific values:

```bash
helm upgrade my-mariadb . -f values.yaml
```

To see what would change before upgrading:

```bash
helm diff upgrade my-mariadb .
```

## Uninstalling the Chart

To uninstall/delete the `my-mariadb` deployment:

```bash
helm uninstall my-mariadb
```

## Configuration

The following table lists the configurable parameters of the MariaDB chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | MariaDB image repository | `mariadb` |
| `image.tag` | MariaDB image tag | `10.4` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `mariadb.rootPassword` | Root password for MariaDB | `changeme` |
| `mariadb.database` | Database name to create | `magento` |
| `mariadb.user` | Database user to create | `magento` |
| `mariadb.password` | Password for the database user | `magento` |
| `service.type` | Kubernetes service type | `ClusterIP` |
| `service.port` | Service port | `3306` |
| `persistence.enabled` | Enable persistence using PVC | `true` |
| `persistence.storageClass` | PVC Storage Class | `""` |
| `persistence.accessMode` | PVC Access Mode | `ReadWriteOnce` |
| `persistence.size` | PVC Storage Request | `10Gi` |
| `resources.limits.cpu` | CPU limit | `1000m` |
| `resources.limits.memory` | Memory limit | `1Gi` |
| `resources.requests.cpu` | CPU request | `500m` |
| `resources.requests.memory` | Memory request | `512Mi` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash
helm install my-mariadb . \
  --set mariadb.rootPassword=secretpassword \
  --set mariadb.database=mydb
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart:

```bash
helm install my-mariadb . -f values.yaml
```

## Persistence

The MariaDB image stores data at the `/var/lib/mysql` path of the container.

By default, the chart mounts a Persistent Volume at this location. The volume is created using dynamic volume provisioning.
