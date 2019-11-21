# Debugging Live Applications the Kubernetes Way: From a Sidecar

| [Background](https://sched.co/Uahb) | [Slides](slides/2019-11_NA_Kubecon_-_Debugging_Live_Applications_in_Kubernetes.pdf) | [GitHub](https://github.com/joe-elliott/netcore-kubernetes-profiling) |
| ----------------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------- |

**Speakers**
* Joe Elliott, Grafana Labs

This talk will discuss perf tools available, and how to use these tools from a
sidecar.

## Why from a sidecar?

* Doesn’t require host access
* Preserves immutability of host
* “Easy” to build a complete toolset
  * Can dynamically add tools on the fly
* Supports development diversity

## "Easy" is relative

* Finding tools/resources that work with your kernel (version) in your sidecar
  * Pull after deployment
  * Bake in tooling
  * Mount from host
* Sidecar image can be very large
* Sidecars can’t be added dynamically
  * Pod spec is immutable
  * Kubernetes does not allow injecting a sidecar into an already running pod
    * Docker can inject a container at runtime...but would still need SSH
    access

## Pod Features

* shareProcessNamespace
* Sharing mounted volumes
* Mounting host paths
* securityContext.privileged

## CPU Profiling

By sampling and recording the stack many times a second, we can determine which
methods our application spends most of its time in. 

Tools:

* perf
* flamegraphs

Information Gathered:

* Where is my application spending most of its time?
* Why does it have intermittent performance issues?
* What is it doing when the CPU spikes?

## Static Tracepoints

Pre-instrumented events can be captured and stored for later analysis.

Tools:

* LTTng
* Babeltrace
* Trace Compass

Information Gathered:

* When and how often do pre-instrumented events occur?

## Dynamic Tracing

Attach custom tracepoints to uninstrumented code and dynamically record when
and how they are executed.

Tools:

* Perf
* BCC/BPF

Information Gathered:

* When is an arbitrary function called?
* What arguments are passed and what does it return?