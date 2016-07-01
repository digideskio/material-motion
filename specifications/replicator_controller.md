# ReplicatorController specification

This is the engineering specification for the `ReplicatorController` object.

A replicator controller makes use of a `Replicator` instance to create replicas of elements. `ReplicatorController` provides APIs for configuring when replication should and should not occur.

Printable tech tree/checklist:

![](../_assets/ReplicatorControllerTechTree.svg)

---

<p style="text-align:center"><tt>MVP</tt></p>

**Concrete object**: A `ReplicatorController` is a concrete object.

Example pseudo-code:

    ReplicatorController {
    }

**Replicator API**: Provide an API for setting a replicator instance.

The replicator instance performs the actual replication.

> Consider providing a default replicator instance that performs a "best-effort" replication.

Example pseudo-code:

    ReplicatorController {
      var replicator: Replicator
    }

**Disable replication API**: Provide an API for disabling replication of specific elements.

The controller maintains a permanent list of elements that will not be replicated. We will refer to this as the list of disabled elements.

Elements are assumed to be replicable by default. Do not replicate elements for which replication was disabled.

Example pseudo-code:

    ReplicatorController {
      function disableReplicationForElement(Element element)
    }

**Replication API**: Provide an API for replicating an element.

This API should accept an element and return either an element or null.

The implementation of this API first consults the list of disabled elements. If the element is present, the API returns null. If the element is not present, the controller invokes the assigned replicator's `replicateElement` API.

Example pseudo-code:

    ReplicatorController {
      function createReplica(Element element) -> Element or null {
        if disabledElements.contains(element) {
          return null
        }
        return replicator.createReplica(element)
      }
    }

<p style="text-align:center"><tt>/MVP</tt></p>

---