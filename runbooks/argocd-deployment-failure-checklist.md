# ArgoCD Deployment Failure Checklist (Quick Triage)

Use this when a team says: "ArgoCD deployment failed / app not syncing".

## Step 0 — Capture the minimum info
- Application name:
- Environment:
- Namespace:
- Destination cluster name:
- Repo + branch:
- Error snippet from ArgoCD Events:

## Step 1 — Look at the FIRST error in ArgoCD
ArgoCD UI → Application → Events/Conditions
Focus on the first "failed to ..." message.

## Step 2 — Match the symptom to common patterns

### A) Namespace missing
Symptoms:
- "namespaces <x> not found"
Fix:
- Create namespace, then re-sync

### B) Values file missing / wrong path
Symptoms:
- "failed to generate manifest" + "no such file or directory"
Fix:
- Correct values file reference or repo structure

### C) Destination cluster mismatch
Symptoms:
- "cluster <x> not found"
Fix:
- Correct destination.name or register the cluster

### D) RBAC forbidden
Symptoms:
- "forbidden: cannot create resource ..."
Fix:
- Update RBAC or adjust deployment pattern

### E) Sync hook job failed
Symptoms:
- "hook / Job <x> failed"
Fix:
- Check Job logs; fix missing secret/dependency; re-sync

## Step 3 — Verification
- App becomes Synced and Healthy
- Expected workloads exist in the namespace

## Step 4 — Prevention
- If repeated: create/update runbook
- If doc gap: create doc-gaps entry
- If automatable: create enhancement-idea entry
