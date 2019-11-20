# Admission Webhooks: Configuration and Debugging Best Practices

| [Background](https://sched.co/UaVt) | [Slides](slides/Admission_Webhooks_Configuration_and_Debugging_Best_Practices.pdf) |
| ----------------------------------- | ---------------------------------------------------------------------------------- |

**Speakers**
* Haowei Cai, Google

The slides for this talk contain a lot of good information and examples.

## What is an Admission Controller?

There are two types:
* Mutating
  * May change the request, as well as allow or deny the request
* Validating
  * May not change the request, only allow or deny the request

_Mutating webhooks_ are run sequentially first, before the
_validating webhooks_ are run in parallel.

## Webhook Best Practices

* Idempotence
  * Ordering is hard, it can be possible that some mutating webhooks should run
  before others do
* Intercept all versions of an object
  * For example with Deployment API:
    * extensions/v1beta1
    * apps/v1beta1
    * apps/v1beta2
    * apps/v1
* Availability
  * Time calling webhook builds-up time completing API requests
  * Recommended for webhooks to have a 2 second timeout
* Guaranteeing the final state of the object is seen
  * If you use a mutating webhook to enforce security policy, make sure to use
  a validating webhook to ensure that.
* Side effects
  * Avoid side effects if possible
  * Have a reconciliation mechanism (e.g. a controller) in case the request
  didn’t make it through
  * Don’t trigger the side effect in dry run
* Avoiding operating on the kube-system namespace
  * Safety (system-critical components)
    * `kube-apiserver` post-start hooks
    * Control plane components
      * Service accounts
      * kube-dns
  * Efficiency

## How to Debug Webhooks?

| Failure Category     | Valid Webhook Rejection                        | Error Calling Webhook                                 | Error Calling Webhook (failurePolicy: Ignore)         | apiserver internal error   |
| :------------------: | :--------------------------------------------: | :---------------------------------------------------: | :---------------------------------------------------: | :------------------------: |
| What Happened        | 403 webhook forbids/500 webhook internal error | Timeout/Connection failure/Malformed webhook response | Timeout/Connection failure/Malformed webhook response | apiserver internal timeout |
| End-User HTTP Status | 403/500                                        | 500                                                   | No error                                              | 500                        |  

## Metrics

Metrics are provided via apiserver's /metrics endpoint

* Apiserver_admission_webhook_admission_duration_seconds
  * Histogram metrics
* Apiserver_admission_webhook_rejection_count
  * Counter metrics
    * Name
    * Operation
    * Type
    * Error type
    * Rejection code

## Audit Logging

| [Reference documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/) |
| -------------------------------------------------------------------------------------------- |

Example audit Policy object yaml:

```yaml
apiVersion: audit.k8s.io/v1 # This is required.
kind: Policy
# Don't generate audit events for all requests in RequestReceived stage.
omitStages:
  - "RequestReceived"
rules:
  # Log pod changes at RequestResponse level
  - level: RequestResponse
    resources:
    - group: ""
      # Resource "pods" doesn't match requests to any subresource of pods,
      # which is consistent with the RBAC policy.
      resources: ["pods"]
  # Log "pods/log", "pods/status" at Metadata level
  - level: Metadata
    resources:
    - group: ""
      resources: ["pods/log", "pods/status"]
```

* Annotations key-value pairs
  * “mutation.webhook.admission.k8s.io/round_{}\_index\_{}”
    * Value contains true/false if a mutation was applied
  * “patch.webhook.admission.k8s.io/round_{}\_index\_{}”
    * Value contains the JSONPatch contents applied

# Webhook Logging

Have good logging in the webhook backend
* What AdmissionReview it got
* What AdmissionResponse it responded with

## Key Takeaways

* Configure your admission webhooks following the best practices
* Use metrics and audit logging to monitor and debug your webhooks