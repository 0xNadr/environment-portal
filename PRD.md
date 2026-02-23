# Environment Portal - Product Requirements Document

## Overview

A simple status portal deployed via GitOps to demonstrate ArgoCD and OpenShift capabilities.

## Problem Statement

Need a straightforward demo to show:
- GitOps workflow (Git push → automatic deployment)
- Multi-environment deployments (dev/prod)
- ArgoCD self-healing and sync features
- OpenShift routes and deployments

## Solution

A single nginx container serving a static HTML page with environment-specific content.

| Environment | Branding | Message |
|-------------|----------|---------|
| Dev | Blue theme | "Development Environment" |
| Prod | Green theme | "Production Environment" |

## Features

### Must Have
- [ ] Single HTML page showing environment name
- [ ] Different color themes per environment
- [ ] ConfigMap-driven content (easy to change via Git)
- [ ] OpenShift Route for external access

### Demo Scenarios
1. **Deploy** — Apply ArgoCD apps, watch both environments spin up
2. **Update** — Change HTML in Git, ArgoCD syncs automatically
3. **Self-Heal** — Delete a pod, watch ArgoCD restore it
4. **Drift Detection** — Manually edit deployment, see ArgoCD flag it

## Technical Approach

```
Git Repo
├── base/           # Shared deployment, service, route
└── overlays/
    ├── dev/        # Dev ConfigMap (blue HTML)
    └── prod/       # Prod ConfigMap (green HTML)
```

- **Kustomize** for environment overlays
- **ConfigMap** holds the HTML content
- **ArgoCD Application** per environment

## Success Criteria

- Both environments accessible via OpenShift routes
- Changing Git content updates the portal within 3 minutes
- Deleting a pod results in automatic recreation
- ArgoCD UI shows sync status for both apps

## Out of Scope

- Authentication
- Database
- Backend API
- CI/CD pipelines (just GitOps)
- Monitoring/logging setup

## Prerequisites

- OpenShift cluster (4.x)
- OpenShift GitOps operator installed
- Git repository (GitHub/GitLab)
- `oc` CLI access
