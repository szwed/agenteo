# Controller Archetypes

Four archetypes for how controllers interact with resources in the Kubernetes API-centric (not API-driven) architecture.

## Actuators

Map real-world capabilities into virtual world via [digital twins](Digital-Twins.md). Examples: **kubelet** (registers node, watches assigned Pods), [Crossplane](Crossplane.md), ExternalDNS. Crossplane Providers are the classic actuator pattern: each Provider controller watches its managed resources (KRM CRDs) and reconciles them to real cloud resources via cloud APIs, mapping external state into the Kubernetes digital twin model.

## Attribute Controllers

Operate in virtual world on existing digital twins. Enrich/calculate attributes managed by other controllers. Examples: **Scheduler** (computes `Pod:spec:nodeName` assignment from Node and Pod objects), Gatekeeper, Kyverno.

## Aspect Controllers

Handle specific aspects of a resource, potentially targeting a different environment than the main controller. Example: **Service** -- main controller handles cluster-internal routing; a separate aspect controller instructs a LoadBalancer in IaaS. Main functionality exists without the aspect.

## Logical Object Controllers

Operate in virtual world only, introducing new abstract types. All custom operators fall here. Examples: **ReplicaSet** (ensures stable replica count of Pods), **Deployment** (instruments ReplicaSet for rolling updates, rollback, scaling).
