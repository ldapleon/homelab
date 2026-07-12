# Monitoring

## Metrics Server

Metrics Server provides Kubernetes resource metrics for tools such as `kubectl top`, Headlamp and HPA.

Installed via Flux HelmRelease.

### Validation

```bash
kubectl top nodes
kubectl top pods -A
kubectl get apiservice v1beta1.metrics.k8s.io