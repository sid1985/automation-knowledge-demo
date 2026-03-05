# ArgoCD Sync Failure – Sync hook job failed

## Problem
ArgoCD Application shows Degraded after sync. Most resources created, but sync fails at the end.

## Platform
ArgoCD / AKS

## Error Message
Sync failed: hook / Job "db-migrate" failed

## Root Cause
A PreSync/Sync/PostSync hook job failed (often due to missing secrets/config, or dependency not ready).

## Fix
1. In ArgoCD Application → Resource Tree, locate the failing Job.
2. Check Job logs:
   kubectl -n <namespace> logs job/<job-name>
3. Resolve missing secret/config or dependency readiness issue.
4. Re-run sync (or rerun job if your pattern allows).

## Prevention
- Add readiness checks for dependent services.
- Ensure secrets/config required by hook jobs are provisioned before sync.
- Add a runbook section specifically for hook failures.

## Automation Opportunity
Add automated log extraction for failed hook jobs and attach to DTR case template.
