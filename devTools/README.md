# Use Your Favorite Developer Tools in Kubernetes With Telepresence

| [Background](https://sched.co/UaeA) | [Slides](slides/Use_Your_Favorite_Developer_Tools_With_Telepresence.pdf) | [Telepresence](https://www.telepresence.io/) |
| ----------------------------------- | ------------------------------------------------------------------------ | -------------------------------------------- |

**Speakers**
* Abhay Saxena, Datawire

Debugging and testing can be hard, especially if you have to wait to deploy.
Telepresence can help by providing tools to make your local environment think
it's in the cluster.

Telepresence can replace a deployment in Kubernetes with a proxied instance,
which routes requests back to your local environment. This can
allow for using a debugger in an IDE or CLI.

Telepresence also allows for proxying a particular container within a pod,
and allow runtime redirection of connections to `localhost` to be caught and
routed to the pod.

The proxy supports TCP traffic, more than just HTTP. If the protocol is HTTP
however, Telepresence can be set to intercept requests with matched headers and
allow the unmatched requests through.
 