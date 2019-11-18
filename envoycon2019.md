# EnvoyCon 2019

## Welcome, Thank You, Growth

| [Background](https://sched.co/UxvJ) |
| ----------------------------------- |

* Speakers
  * Matt Klein, Lyft

Envoy is a extensible proxy with many other products are built upon it. Envoy
was built with a very rapid velocity, but needs to transition into a more
sustainable, long-term approach for future growth.

Envoy recognizes that its API is the most important part, and that the proxy is
an implementation detail. There was been recent investment in improving
security with help from Google, however improving security affects velocity.

Envoy wants help from the open-source community with maintaining the project,
code reviews, documentation, etc.

## How Spotify Migrated Ingress HTTP Systems to Envoy

| [Background](https://sched.co/Uxv2) | [Link to slides](slides/atc_envoycon_2019.pdf) |
| ----------------------------------- | ---------------------------------------------- |

* Speakers
  * Alex Sundström, Spotify
  * Erik Lindblad, Spotify
  * Kateryna Nezdolii, Spotify

They migrated to Envoy in their "perimeter", i.e. they line between the
internet and their internal services.

They learned a lot in migration effort, in particular how useful it was to have
a "big red button" to roll back changes that anyone could hit.

## Envoy Mobile in Depth: From Server to Multi-platform Library

| [Background](https://sched.co/UxvS) | [Envoy Mobile](https://envoy-mobile.github.io/) | [GitHub](https://github.com/lyft/envoy-mobile) |
| ----------------------------------- | ----------------------------------------------- | ---------------------------------------------- |

* Speakers
  * Jose Nino, Lyft
  * Michael Schore, Lyft

Why Envoy on mobile? Lyft is looking to extent all of the benefits that Envoy
provides for backend services, to their mobile platform/application. The idea
is to treat mobile devices like any other node in a network topology.

To accomplish this across multiple mobile platforms, they went to change Envoy
into a library rather than just a single process.  This would allow for
standardization across all platforms, with common tooling for common problems,
and reduced cognitive load.

Designing a mobile approach meant including support for many different
languages. For example, Envoy is C++, Android is Kotlin, iOS is Swift, C
bindings as a common bridge across them all. The multithreading design required
a significant amount of thinking, not just about how to convert the existing
Envoy multithreaded process into a thread that can be run by another program as
a library, as well as how to allow native handling of threads and callbacks
across platforms.

Another big advantage is gaining the observability that Envoy provides for
mobile devices, something that was missing from their full picture of metrics
gathering.

Going forward, they want to further refine Envoy Mobile as a drop-in replacement
for other platform-specific implementations. They also want to explore protocol
experimentations, intelligent network behavior (health checks/load balancing,
as well as across interfaces like choosing between wifi/cell networks,
protocols, and IPv4 vs IPv6 for best performance). They also want to implement
dynamic configuration.
 
## Envoy’s Using 10GB of Memory and It’s All My Fault!

| [Background](https://sched.co/UxvT) | [Link to slides](slides/Envoycon2019_10GBMemory.pdf) | [Contour](https://projectcontour.io/) | [GitHub](https://github.com/projectcontour/contour) |
| ----------------------------------- | ---------------------------------------------------- | ------------------------------------- | --------------------------------------------------- |

* Speakers
  * Steve Sloka, VMware

Contour is an ingress controller for Kubernetes. It runs all traffic through
Envoy. VMware found Contour was using very high levels of memory from what was
expected and learned some interesting characteristics during their debugging. 

Changes to Secrets (e.g. Certificates) caused updates to LDS. High rate of
changes caused lots of old configurations that needed to be drained from
listeners. Listeners had a default drain timeout of 600s and held onto memory
during the drain.

## Envoy Namespaces - Operating an Envoy-based Service Mesh at a Fraction of the Cost

| [Background](https://sched.co/UxvY) | [Cilium](https://cilium.io/) | [GitHub](https://github.com/cilium/cilium) |
| ----------------------------------- | ---------------------------- | ------------------------------------------ |

* Speakers
  * Thomas Graf, Cilium / Isovalent

Cilium with Envoy via Sidecar pattern in Kubernetes.

Shift to have one Envoy per Node, instead of per Pod, to alleviate scaling
issues.

The concept of "namespaces" for Envoy is to allow fair sharing of the Node
Envoy across the client pods.

Development is happening in SIG-Envoy.

## Managing Tens of Thousands of Envoy: How We Do It

| [Background](https://sched.co/WjiG) | [Link to slides](slides/AWSAppMesh_EnvoyCon.pdf) |
| ----------------------------------- | ------------------------------------------------ |

* Speakers
  * Shubha Rao, AWS

## Spanning the Globe with Envoy at Stripe

| [Background](https://sched.co/Uxve) | [Links to slides](slides/dylan-carney-envoycon.pdf) |
| ----------------------------------- | --------------------------------------------------- |

* Speakers
  * Dylan Carney, Stripe

Stripe is a technology company that builds economic infrastructure for the
internet.

TLS negotiation is expensive, especially when client and server are physically
far from each other over the internet. To solve this, they employ Envoy near
clients around the world and their servers in the US for mTLS and HTTP/2.
HTTP/2 in particular is useful for multiplexing requests over a single TCP
connection.

They use blue/green deployments, where traditionally 100% of traffic goes to
one deployment, and components can be upgraded on the other before cutting
clients over.  With Envoy, they can route a certain percentage of traffic
across both environments to prevent issues from client-side DNS caching. They
can also route requests away from bad hardware/software deployments while they
remediate.

## From Microbenchmarks to HTTP2 Load-testing: 5 Performance Tools and Techniques to Improve Envoy Scalability

| [Background](https://sched.co/Uxvn) | [Links to slides](slides/EnvoyCon_Perf_Tools_2019_v1.pdf) | [Google Benchmark GitHub](https://github.com/google/benchmark) | [Nighthawk GitHub](https://github.com/envoyproxy/nighthawk) |
| ----------------------------------- | --------------------------------------------------------- | -------------------------------------------------------------- | ----------------------------------------------------------- |

* Speakers:
  * Joshua Marantz, Google
  * Otto van der Schaaf, We-Amp B.V.

Information-packed presentation with a lot more details in the slides.

They added C++ macros to enable performance monitoring and found a lot of time
was being spent in regular expression matching misses.

They also designed an HTTP load generator called `Nighthawk` to evaluate Envoy
performance.

They also used fuzz testing techniques to find performance and security issues
with Envoy, however the fuzz testing is slow to run.

## Service Mesh in Kubernetes: It’s Not That Easy

| [Background](https://sched.co/Uxvo) | [Links to slides](slides/EnvoyCon_2019_Lita_Tom.pdf) |
| ----------------------------------- | ---------------------------------------------------- |

* Speakers
  * Lita Cho, Lyft
  * Tom Wanielista, Lyft

Prior to Kubernetes adoption within Lyft, they implemented a means of service
discovery on their existing infrastructure.  To help with their internal
migration to Kubernetes, they designed a control-plane mechanism that exists
outside of Kubernetes to allow legacy infrastructure and Kubernetes deployments
to continue to discover each other. This is accomplished by the control-plane
watching for events from `apiserver` for the components moved into Kubernetes
and the components reaching out to the control-plane to discover the services.

They ran into issues with Kubernetes Pod scale up and down events, as well as
the order of operations in which sidecars run, so they currently run a patched
version of Kubernetes with some fixes they need.
