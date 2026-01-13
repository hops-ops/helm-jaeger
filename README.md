# helm-jaeger

A Crossplane Configuration package that installs the Jaeger Helm chart with a minimal, stable interface.

## Overview

`helm-jaeger` renders a single Helm release for Jaeger. It exposes only the inputs needed
for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<clusterName>-jaeger` in the `jaeger` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.2)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-jaeger
spec:
  package: ghcr.io/hops-ops/helm-jaeger:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: Jaeger
metadata:
  name: jaeger
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    allInOne:
      enabled: true
    storage:
      type: memory
```

## Development

```bash
make render
make validate
make test
```
