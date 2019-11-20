# Are You About to Break Prod? Acceptance Testing with Ephemeral Environments

| [Background](https://sched.co/UaWE) | [Slides](slides/KubeCon_-_Are_you_about_to_break_prod.pdf) | [GitLab](https://gitlab.com/rocore/demo-app/) |
| ----------------------------------- | ---------------------------------------------------------- | --------------------------------------------- |

**Speakers**
* Erin Krengel, Pulumi
* Sean Holung, Nordstrom

## Types of Testing

Two kinds in this context:

* Unit testing
  * These test specific functions in code
* Acceptance testing
  * These test components in a system

## Ephemeral Environments

Automate acceptance testing with spinning up ephemeral environments.

Use automation tools for building environments so that CI can create the
ephemeral environment for running the tests. The ephemeral environment should
match production as closely as possible.

The acceptance tests can be written in code and run as Kubernetes jobs.

## Benefits

* Ensures service behaves as expected
* Documents behavior
* Provides confidence to make sweeping changes
* Tests applications & infrastructure
* Quicker feedback loops
* Reproducible environment that mimics Prod
* Encourages automated testing
