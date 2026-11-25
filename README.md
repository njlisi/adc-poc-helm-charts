# ADC POC Helm Charts

Minimal, security-hardened Helm charts for deploying sample containerized ADK agents onto GKE Autopilot via Google Cloud Application Design Center (ADC) Native Helm.

## Charts

- `charts/financial-advisor`: Deploys the public sample `financial-advisor` ADK container with:
  - Chart-managed Workload Identity Kubernetes ServiceAccount (`iam.gke.io/gcp-service-account`)
  - Private `ClusterIP` service (no public ingress/LoadBalancer exposure)
  - Hardened container `securityContext` (`allowPrivilegeEscalation: false`, `capabilities.drop: ["ALL"]`, `seccompProfile: RuntimeDefault`)
  - Startup, readiness, and liveness probes on `/list-apps`
  - Offline `uv` startup flags (`UV_OFFLINE=1`, `UV_NO_SYNC=1`) for private clusters
  - Zero embedded credentials or secrets
