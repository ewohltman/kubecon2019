# Intro: Linkerd

| [Background](https://sched.co/UaiT) | [Slides](slides/Intro_to_Linkerd_Kubecon_2019_NA.pdf) | [Linkerd](https://linkerd.io/) |
| ----------------------------------- | ----------------------------------------------------- | ------------------------------ |

**Speakers**
* William Morgan, Buoyant

Linkerd is an open-source service mesh CNCF project. It is designed to give
platform-wide observability, reliability, and security without requiring
configuration or code changes.

## What does Linkerd do?

Three main areas of focus:

* Observability
  * Service-level golden metrics: success rates, latencies, throughput. Service
  topologies.
* Reliability
  * Retries, timeouts, load balancing, circuit breaking 
* Security
  * Transparent mTLS, cert management and rotation, policy

All in an ultralight package focused on operational simplicity first and
foremost.

## Why should I care?

Linkerd gives platform owners (SREs, architects) the observability,
reliability, and security primitives that are critical for cloud native
architectures with no developer involvement!

Linkerd doesn't just solve technical problems, it solves _socio-technical_
problems. By decoupling the developers, it gives platform owners control over
their destiny.

## How is Linkerd designed?

| [Control Plane GitHub](https://github.com/linkerd/linkerd2) | [Data Plane GitHub](https://github.com/linkerd/linkerd2-proxy) |
| ----------------------------------------------------------- | -------------------------------------------------------------- |

In short, "do less, not more".

* Just works
  * Zero config, out of the box, for any Kubernetes app
* Ultralight
  * Introduce the bare minimum perf and resource cost
* Simple
  * Reduce operational complexity in every possible way

Components:

* Control plane
  * Go. ~200mb RSS (excluding metrics data)
* Data plane
  * Rust. <10mb RSS, <1ms p99 (!!!) 