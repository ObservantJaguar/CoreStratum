---
title: Force a Kubernetes Pod Rollout
parent: Recipes
grand_parent: Guides
---

# Force a Kubernetes Pod Rollout

## Goal

Restart all pods of a workload so they pick up a new ConfigMap/Secret without editing the Deployment.

## Task

Deployment pods still run the old values after a ConfigMap was updated; restart the pods to reload the new ones.

## Steps

1. Trigger a rollout (creates new ReplicaSet, replaces pods):

```bash
kubectl rollout restart deployment/app
```

2. Watch it complete:

```bash
kubectl rollout status deployment/app
```

3. Alternative - patch the pod template with an annotation (also forces a new ReplicaSet):

```bash
kubectl patch deployment app -p '{"spec":{"template":{"metadata":{"annotations":{"kubectl.kubernetes.io/restartedAt":"2026-10-08T09:00:00Z"}}}}}'
```

4. Take down / scale back up for StatefulSets or when a full restart is wanted:

```bash
kubectl rollout restart statefulset/app
kubectl rollout restart daemonset/agent
```

## Verification

- New pods appear and old ones terminate:

```bash
kubectl get pods -w
```

- The rollout reports success:

```bash
kubectl rollout status deployment/app
```

- Confirm the new value inside a running pod:

```bash
kubectl exec deploy/app -- env | grep MY_VAR
```

## Gotchas

- **Restart does not reload the file for you** - a `volumeMount` of a ConfigMap is updated by the kubelet, but an environment variable taken from `env`/`envFrom` is baked in when the pod starts. `rollout restart` only helps if the app re-reads the mounted volume; for env vars you need a controller/watch that reloads them, or an app that watches the mount.
- **`volumeMounts` vs `env`** - prefer mounting ConfigMaps as volumes when you want live updates; `env` values require a pod restart and, even then, only help if the app picks up the change.
- **DaemonSets** - `kubectl rollout restart daemonset/<name>` works the same way, so also restart node agents after config changes.
- **Nothing changed = no rollout** - if neither the image nor the template changed, a restart may produce a new ReplicaSet with identical pods; verify by `kubectl get rs` or the annotation timestamp.

## Related

- [Kubernetes workloads](../../orchestration/schedulers/kubernetes.md)
- [ConfigMaps and Secrets](../../orchestration/package-management/helm.md)