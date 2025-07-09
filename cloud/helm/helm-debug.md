# TIL: How to Debug and Dry-Run a Helm Chart

## 🔍 Helm Debugging Tips

When working with Helm charts, especially custom ones, it's important to validate and debug them **before** deploying.

### 🚀 Dry-Run a Helm Chart

Use the `--dry-run` and `--debug` flags to render templates locally without deploying to the cluster.

```bash
helm install my-release ./my-chart --dry-run --debug
```

This will:

- **Render** the templates with values.
- **Print** the full manifest to stdout.
- **Validate** Kubernetes schema (if Helm is connected to a cluster).