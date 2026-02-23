# Environment Portal

A simple status portal deployed via GitOps to demonstrate ArgoCD and OpenShift capabilities.

## What It Does

Deploys a single nginx container serving a static HTML page with environment-specific content:

| Environment | Theme | Message |
|-------------|-------|---------|
| Dev | Blue | "Development Environment" |
| Prod | Green | "Production Environment" |

## Demo Scenarios

1. **Deploy** — Apply ArgoCD apps, watch both environments spin up
2. **Update** — Change HTML in Git, ArgoCD syncs automatically
3. **Self-Heal** — Delete a pod, watch ArgoCD restore it
4. **Drift Detection** — Manually edit deployment, see ArgoCD flag it

## Project Structure

```
├── base/           # Shared deployment, service, route
└── overlays/
    ├── dev/        # Dev ConfigMap (blue HTML)
    └── prod/       # Prod ConfigMap (green HTML)
```

## Tech Stack

- **Kustomize** for environment overlays
- **ConfigMap** for HTML content
- **ArgoCD Application** per environment

## Prerequisites

- OpenShift cluster (4.x)
- OpenShift GitOps operator installed
- `oc` CLI access

## Quick Start

1. Clone this repo
2. Apply the ArgoCD applications
3. Access the portals via OpenShift routes

## License

MIT
