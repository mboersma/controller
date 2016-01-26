# Release Checklist

## Testing Goals

When a change is proposed to a Deis platform component, it must first pass testing. In addition to
unit tests on the component code base and functional tests on the packaged component, end-to-end
(e2e) tests must be run to ensure that the change integrates successfully with the rest of the Deis platform. (But maybe not always: see "Future Testing Optimization")

When a change is merged to a Deis platform component, end-to-end tests are run on the entire
platform. Assuming those e2e tests pass, the set of components tested are considered a new release.
There are two types of releases, depending on the origin of the change.

### Canary Releases

When a change is merged to the master branch of a Deis platform component, it initiates a
potential "canary" release. End-to-end tests begin from the `git` SHA of the change. That
component is tested in integration with the other canary components. If e2e tests pass, the
SHA is considered the new canary version for that component. If the tests fail, the canary
version for that component remains as before, and the development team is notified of an
integration failure.


### Tagged Releases

When a semantic-versioned tag is pushed to the master branch of a Deis platform component,
it initiates a potential official release. End-to-end tests begin from the `git` tag. That
component is tested in integration with the most recently passed tags for other components.
If e2e tests pass, 

If a semantic-versioned git tag is pushed to the deis/workflow component (for example), e2e
tests are started based on that tag in the deis/workflow project. This is a potential external
release of the Deis platform.

To set up e2e testing for a tagged release,


## Example Release



### Future Testing Optimization

Running end-to-end tests against a real Kubernetes cluster is necessarily expensive in terms
of time. It is also to be expected that the e2e tests will slow down as they are expanded, or at
least that running e2e tests on every code submission will represent a bottleneck to an efficient
CI process.

As the contracts and interfaces between components solidify, per-component unit tests and
functional tests must grow. When those local tests mature and demonstrate sufficient coverage,
they may be considered enough to pass a proposed code change without involving e2e tests.

## Release Goals

Once a proposed change has passed testing,
