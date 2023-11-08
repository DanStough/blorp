# blorp
BLORP, or maybe Universal Consul Dev Environment

## Intro
 
### Purpose
To shorten the feedback loop of the Consul development cycle, starting with a focus/integration on K8S.

### Non-purpose
1. Simulate all deployments of Consul

### Benefits
1. K8S Testings First
2. Faster :runner:
    - uses existing docker containers and replaces only the binary
    - [pushes containers around locally](https://skaffold.dev/docs/environment/local-cluster/) - no remote registries required.
    - concurrent builds
    - less typing
3. Implicitly tests "upgrade" scenarios. Re-deploying Consul on top of Consul.
4. Some conveniences, like default port forwarding.

### Cons
1. Obviously only works for k8s
2. Moving between versions could be hard (could be solved with different branches or clusters)
3. Still requires additional configurations for failover, etc.

## How to use the thing

1. Make sure you have a kubernetes cluster and cli accoutrements installed and configured properly.
Tools I recommend when in doubt:
   1. [Rancher Desktop](https://rancherdesktop.io/) with the Moby container runtime selected. This will also install 
   1. [k3d](https://k3d.io/) for creating a cluster with multiple nodes, which is useful for deployments in Consul that have anti-affinity. 
   I use this one for testing. I use this for testing: `k3d cluster create testing --agents=3 --no-lb`
1. Install [Skaffold](https://skaffold.dev/docs/install/) >=v2.0
    1. Easy mode: `brew install skaffold`
1. Clone this repo.
1. Initialize the submodules:
   1. `git submodule init`
   1. `git submodule update`
1. Run the following command.
    1. `skaffold dev``
1. ☕️
1. Change a file affecting one of the Consul components and watch the helm chart redeploy.
<!-- 1. Visit the Consul UI at [http://localhost:8080](http://localhost:8080) -->
1. Visit the FakeService App at [http://localhost:8081](http://localhost:8081) -->
1. When you're done, CTRL+C to exit skaffold and have it clean up your cluster.

## TODO
- [ ] Have applications redeploy when consul-dataplane is redeployed
- [ ] Experiment with a go.work file at the root of the repo to share the API module.
- [ ] Build the UI
- [ ] Build CRDs and check for to redeploy
- [ ] Codespace Integration?

