# EnvoyCon 2019

## Welcome, Thank You, Growth

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

[Background](https://sched.co/Uxv2)

[Link to slides](slides/atc_envoycon_2019.pdf)

* Speakers
  * Alex Sundström, Spotify
  * Erik Lindblad, Spotify
  * Kateryna Nezdolii, Spotify

They migrated to Envoy in their "perimeter", i.e. they line between the
internet and their internal services.

They learned a lot in migration effort, in particular how useful it was to have
a "big red button" to roll back changes that anyone could hit.

## Envoy Mobile in Depth: From Server to Multi-platform Library

[Background](https://sched.co/UxvS)

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
 