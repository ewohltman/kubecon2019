# Take Envoy Beyond a K8s Service Mesh - to Legacy Bare Metal and VMs + More

| [Background](https://sched.co/Uadj) | [Slides](slides/KubeCon_NA_2019_-_Take_Envoy_beyond_a_K8s_service_mesh.pdf) |
| ----------------------------------- | --------------------------------------------------------------------------- |

**Speakers**
* Steve Sloka, VMware
* Steven Wong, VMware

Envoy’s mission is to extract network and communication security code from
applications in a way that developers and users can deploy components that just
work no matter where they run or what hosts them.

This session will show how to leverage Envoy to achieve interoperation of
applications and services, split across Kubernetes and traditional VM or bare
metal hosts. We’ll look at how to incrementally bring Kubernetes into an
existing application architecture based on existing VM or bare metal
applications and services.

Specific examples will demonstrate:
* Using Contour with Envoy as an Ingress and load balancer solution with a
richer feature set than some common alternatives
* Sending requests from VM workloads to Kubernetes services
* Direct requests to services running on a VM from Kubernetes
* Dynamical traffic steering - K8s and VM workloads at the same time

## Why Envoy/Service Mesh?

* It makes tracking where services exist easier
* Helps knowing if endpoints are healthy
* App developers are usually not networking or security experts

## What is Envoy?

| [Envoy](https://www.envoyproxy.io/) | [GitHub](https://github.com/envoyproxy/envoy) |
| ----------------------------------- | --------------------------------------------- |

Envoy is an open source edge and service proxy, designed for cloud-native
applications.

Goal:
* Move network details+code out of application - make network transparent to
app devs and users

Architecture Emphasis:
* API driven; dynamic configuration support
* Top notch support for observability and debugging 

## What is a Service Mesh?

* Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic
* Fine-grained control of traffic behavior with rich routing rules, retries, failovers,
and fault injection
* A pluggable policy layer and configuration API supporting access controls,
rate limits and quotas
* Automatic metrics, logs, and traces for all traffic within a cluster, including
cluster ingress and egress
* Secure service-to-service authentication with strong identity assertions
between services in a cluster

## What is Contour?

| [Contour](https://projectcontour.io/) | [GitHub](https://github.com/projectcontour/contour) |
| ------------------------------------- | --------------------------------------------------- |

Kubernetes Ingress Controller that leverages Envoy as the data plane:
* Dynamically updated load balancing configuration without dropped
connections
* Safely supports ingress in multi-team Kubernetes clusters
* Enables delegation of routing configuration for a path/header or domain to
another Namespace
* Flexibly defines service weighting, load balancing strategies, and more
without annotations

_Contour is not a Service Mesh._

## What is Gimbal?

| [Gimbal](https://github.com/vmware-tanzu/gimbal) |
| ------------------------------------------------ |

Gimbal is a layer-7 load balancing platform built on Contour, which is an
Ingress controller for Kubernetes that works by deploying the Envoy proxy as a
reverse proxy and load balancer. It provides a scalable, multi-team, and
API-driven ingress tier capable of routing Internet traffic to multipl
upstream Kubernetes clusters and to traditional infrastructure technologies
such as OpenStack.

## More information

More in-depth information and examples can be found in the slides.