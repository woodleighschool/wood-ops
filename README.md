# wood-ops

Each cluster runs its own Flux, pointed at `kubernetes/clusters/<cluster>`.

- `kubernetes/clusters/<cluster>`: `cluster-settings` (storage classes, backup
  bucket, cluster name) and `cluster-apps`, which substitutes them everywhere.
- `kubernetes/apps/<cluster>`: what the cluster runs, one Flux Kustomization per
  app. Cluster-specific config is a component next to it.
- `kubernetes/apps/base`: the apps.
- `talos`: shared machine config, and each cluster's own under `talos/<cluster>`.

Tasks act on the current kube context (`kubectl config use-context sc`, then
`mise run //talos:apply-node k8s-1`), or on `CLUSTER` for a cluster without a
context yet; bootstrap takes the cluster as an argument. Kubeconfig and
talosconfig contexts are named after the cluster. A new cluster copies `kubernetes/clusters/sc`, a trimmed
`kubernetes/apps/sc` and `talos/sc`, with its own 1Password vault, age key and
backup bucket.

---

### 🙌 Credits

Everything in this repo is based on the awesome work at [onedr0p/home-ops](https://github.com/onedr0p/home-ops)
