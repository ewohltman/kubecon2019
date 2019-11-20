# Deep Dive Into API Machinery

| [Background](https://sched.co/Uahb) |
| ----------------------------------- |

**Speakers**
* Antoine Pelisse, Google
* Stefan Schimanski, Red Hat

SIG API Machinery is discussing a number of topics.
 
 ## CRDs
 
* Immutability in CRDs for either all fields, or individual fields
* How to handle default/null values
* When are JSON objects equal?
  * Rule of thumb: when reflect.DeepEqual() returns true.

Objects can define actor's intent.

Client-side apply would send intent.  Server-side apply would satisfy the
intent.

An object's field can have ownership. If something other than the owner tries
to make a change to an owned field, it will encounter a conflict.

Still a bit away from seeing this realized. There are a number of things still
being worked out (e.g. performance impact to `apiserver`).

## API Priority and Fairness

Overall goal is to protect against buggy or aggressive controllers from
overloading `apiserver`. API calls can have different priority levels to tune
rate-limiting and queuing.

New object type `FlowSchema` can be used for attaching priority to request
types.
