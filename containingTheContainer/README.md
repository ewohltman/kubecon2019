# Containing the Container: Developer Experience vs Strict Security Posture

| [Background](https://sched.co/UaXC) | [Slides](slides/Containing_the_Container.pdf) |
| ----------------------------------- | --------------------------------------------- |

**Speakers**
* Brian Bagdzinski, Verizon
* Sharat Nellutla, Verizon

Verizon operates in a highly secure environment, meaning they are not able to
take advantage of a lot of the tools available for an easy and rapid
Development Experience.

In their first iteration of their internal Development Experience, the did a
lot of their dev work remotely because Docker was not allowed to be run on
developers local machines. They used Docker in Docker techniques with Jenkins
instances for CI, but found Docker in Docker was not very performant and still
carries a risk from the passing of Docker down from parent to child container.

Since then, they have evolved to what they call their DevX 2.0 iteration using
the tools below.

## Development Tools

* Kaniko
  * Builds images in environments that can’t run a Docker daemon
  * Runs within a Kubernetes cluster in an unprivileged state
  * Less performance overhead compared to DinD builds
* Jib
  * Builds optimized images for Java without Docker daemon
  * Splits dependencies from classes into layers -- more granular builds
  * No need for a Dockerfile, plugin via Maven or Gradle
* Skaffold
  * CLI tool that facilitates continuous development for K8s apps
  * Iterate on your code locally then deploy to clusters
  * Can run in background and continually update without input

## Deployment Tools

* GitLab Runners
  * Open source project that is used to run jobs in Gitlab CI
  * Runners can be scoped to projects, groups, or globally
  * Leverage K8s to run builds on a cluster and scale out per job
  * Integration with Kaniko for image builds
* Harbor
  * Open source container image registry
  * Role-based access control for registry and projects
  * Supports integration with image vulnerability scans via Clair
  * Image notary for ensuring authenticity
  * Provides a Helm chart repository

## Analysis Tools

* Octant
  * Web-based tool to view how applications are running on a K8s cluster
  * Easily navigate multiple clusters via contexts and label filters
  * View log streams of pods and containers
  * Forward a local port to a running pod for debugging apps
  * Extensible via plugins
  
* Kui
  * Uses Electron to provide an augmented CLI via kubectl
  * Offers a suite of visualizations for aggregating complex data
  * Gracefully transition between visualizations and console output
  * More easily view and modify JSON and YAML data models
  * Only available for MacOS and Linux