# ArgoCD Sync Failure – RBAC permission denied

## Problem
ArgoCD sync fails when creating resources (namespace, CRDs, cluster-scoped resources).

## Platform
ArgoCD / AKS / Kubernetes RBAC

## Error Message
forbidden: User "system:serviceaccount:argocd:argocd-application-controller" cannot create resource "namespaces" in API group "" at the cluster scope

## Root Cause
ArgoCD controller service account lacks required permissions for the target operation (cluster-scoped or namespace-scoped RBAC missing).

## Fix
1. Identify the resource type being denied (namespaces, clusterroles, CRDs, etc.).
2. Confirm whether the deployment requires cluster-scoped permissions.
3. Apply the required RBAC (ClusterRole/Role + binding) for ArgoCD controller or use an allowed deployment pattern.
4. Re-sync.

## Prevention
- Document which resources are allowed via ArgoCD in your platform.
- Enforce a policy: namespace must exist before onboarding (avoid namespace creation from ArgoCD if not permitted).

## Automation Opportunity
Add a “permission precheck” job that validates ArgoCD controller permissions against required resources (dry-run apply).
