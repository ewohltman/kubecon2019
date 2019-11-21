# Writing a Kubernetes Operator: the Hard Parts

| [Background](https://sched.co/UaeV) | [Slides](slides/Writing_a_Kubernetes_operator_-_the_Hard_Parts_-_KubeCon_2019.pdf) |
| ----------------------------------- | ---------------------------------------------------------------------------------- |

**Speakers**
* Sebastien Guilloux, Elastic

## Kubernetes Operators in a Nutshell

Operators generally work with a CRD that an end-user would apply. The Operator
watches for a create/update/delete event on the watched resource. When an event
occur, a reconciliation is triggered to satisfy the requested CRD
specification.

## Tools and Libraries

* [Kubebuilder](https://github.com/kubernetes-sigs/kubebuilder)
* [controller-runtime](https://github.com/kubernetes-sigs/controller-runtime)

## The Hard Parts

* The operator lives in the past
  * The `apiserver` client uses a _cached reader_ by default
    * Can lead to problems
      * Infinite loops
      * Split-brain situations
      * Double rolling upgrade reaction (delete+recreate pods, then
    delete+recreate the already upgraded pods)
  * _Optimistic concurrency_ is good enough in most cases however
    * Sometimes it can be not enough, especially with stateful workloads
    * If better guaranteed is needed, register expectations in memory and check
    that the cache matches the expectation
  * Best practices
    * Use deterministic naming
    * Always assume a stale cache
    * The entire reconciliation should be idempotent
  * Reconciling resources
    * Hard to do because we can't just use `reflect.DeepEqual` because of
    fields added by Kubernetes/mutating webhooks (e.g. metadata)
    * Custom functions to compare each important field gets messy quickly
    * Better way is to create a hash of the important fields, then compare the
    expected hash against the actual hash
  * Empower users to customize fields in the CRD, but also provide good
  defaults

## StatefulSets

* Cannot resize volumes
* Scheduling conflicts with pods vs. persistent-volumes
  * Can use `volumeBindingMode: WaitForFirstConsumer` for `kind: StorageClass`
* Scheduling conflicts with local volumes vs. resources
* `UpdateStrategy`
  * Choose one: `RollingUpdate.Partition`, `OnDelete`
* You don't have to use StatefulSets
  * You can manage pods and persistent-volume-claims directly  