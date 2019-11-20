# Making an Internal Kubernetes Offering Generally Available

| [Background](https://sched.co/Uab1) | [Slides](slides/Making_an_Internal_Kubernetes_Offering_Generally_Available.pdf) |
| ----------------------------------- | ------------------------------------------------------------------------------- |

**Speakers**
* James Wen, Spotify

Spotify is currently migrating their internal services from Helios to
Kubernetes. This talk covers their experience and learnings they have obtained
during this process. 

## Operation Solidarity

### Multicluster Strategy: Management

_Offload cluster management to an automation tool (e.g. Terraform) or managed
service if possible._

### Multicluster Strategy: Deployment

_Keep it simple for developers to reason about._

They have a deployment abstraction layer (Tugboat) that can deploy to their
previous platform or Kubernetes. They also have a service they call Compass
that determines which Kubernetes cluster(s) applications should be deployed to
(e.g. sticky certain apps to particular clusters, deploy the app to N clusters,
etc.)

### Operational Metrics/Alerts

_Establish trust through monitoring._

* Monitoring on integration components
  * Error
  * Latency
  * Saturation
* Smoke test —> periodic deploys
* Metrics for:
  * Available cluster capacity
  * Status of backups
  * Scheduling

### DiRTing

_Plan for and simulate failures._

* Disaster Recovery Testing
  * Planned and executed DiRTs
    * Cluster deletions
    * Master being down
  * Validation and improvement of
    * Metrics + Alerting
    * Playbooks
    * Backups

## Business Impact

_Track enough data to answer questions._

### Metrics Tracking

Metrics/Dashboard to track:
* Resource Utilization
* Cost
* % apps migrated
* Developer productivity

### Cost Tracking

Cost tracking was an effective motivator for many teams to adopt Kubernetes
on their own. 

## Self-Service

### Self-Service Experience: Namespaces

_Take complexity for your developers._

Allow clients to self-service create namespaces

### Self-Service Experience: Apps

_Use existing tools/abstractions._

Their existing applications had a configuration file for Helios and tooling
(Tugboat) that reads their Helios config to deploy. They extended Tugboat to
also support Kubernetes yaml files, allowing their development teams to migrate
without changing their deployment process.

### Documentation

_You as owners are not the audience._

### Shared Support

_Support can be mutually beneficial._

* Developers will always have questions
* US East Coast + Europe
* Support shifts covering both, where people on these shifts expect to be
interrupted to handle client inquiries/issues

## Feature Parity

_Developers need feature parity or better._

The new Kubernetes offering must have feature parity or more with the
predecessor offering

## Spotify's GA Requirements

* Operational Solidity
* Business Impact
* Self Service Experience
* Important Feature Parity

## Migration & GA Learnings

* Be mindful and deliberate in dictating terminology
* Migrate in stages/series of goals that increase in scope
* Devs will adopt and/or migrate to your Kubernetes offering if it is easy,
complete, and compelling
* Talk to other companies about how they do infrastructure/solve infrastructure
problems
