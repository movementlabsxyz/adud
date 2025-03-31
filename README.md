<div align="center">
  <pre>
a * d
&&
u * d
  </pre>
</div>

# adud

> a = apply
> d = destroy
> u = up
> p = down

`adud` is a standard for defining resource and service lifecycles. 

## Resources
`adud` ensures that Resources have a lifecycle containing an apply and a destroy wherein the following conditions are met:

1. Artifacts produced from an apply MAY parameterize future applies in a partial form. 
2. Artifacts produced from an apply MUST parameterize destroys.

You can learn more about the required relationships from the defined traits [directly](./adud/lifecycle/util/src/lib.rs).

Implementing within the `adud` standard allows you to simply derive lifecycle frontends like the below:

```rust
use clap::Subcommand;
use lifecycle::{LifecycleFrontend, LifecycleSubcommand};
use mcr_protocol_deployer_eth_core::Lifecycle;

#[derive(LifecycleSubcommand, Subcommand)]
#[lifecycle(Lifecycle)]
#[lifecycle_apply_is_subcommand]
#[clap(rename_all = "kebab-case")]
pub enum Eth {}
```

Wherein a `lifecycle_subcommand::Eth` enum is populated with the `apply` and `destroy` subcommands which manage the lifecycle.  

## Services
The same Artifact relationship applies for Services. However, services are expected to continuously run in process, as such the expectation is that artifacts are serialized during the service runtime.

You can learn more about the required relationships from the defined traits [directly](./adud/service/util/src/lib.rs).


## Contributing and getting started

| Task | Description |
|------|-------------|
| [Upcoming Events](https://github.com/movementlabsxyz/ffs/issues?q=is%3Aissue%20state%3Aopen%20label%3Apriority%3Ahigh%2Cpriority%3Amedium%20label%3Aevent) | High-priority `event` issues with planned completion dates. |
| [Release Candidates](https://github.com/movementlabsxyz/ffs/issues?q=is%3Aissue%20state%3Aopen%20label%3Arelease-candidate) | Feature-complete versions linked to events. |
| [Features & Bugs](https://github.com/movementlabsxyz/ffs/issues?q=is%3Aissue%20state%3Aopen%20label%3Afeature%2Cbug%20label%3Apriority%3Aurgent%2Cpriority%3Ahigh) | High-priority `feature` and `bug` issues. |

Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for additional contribution guidelines.

## Organization

There are five subdirectories which progressively build on one another for node logic.

1. [`orfile`](./orfile/): contains all core `orfile` logic.