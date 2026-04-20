# Konfidence Core Concepts

## Artifact

Versioned object from a CI build. Contains a reference to the build result (e.g. Docker image) plus deployment metadata. Does not include the deployable content itself.

## Vector

Complete, immutable specification of desired application state. Contains only references to required artifacts and configurations. Any change creates a new vector.

## Vector Deployment

Explicit instruction to deploy a vector into a specific landscape. Includes full deployment context and status of all referenced artifact deployments.

## Vector Deployment Usage

Defines the lifecycle of a deployment. Determines whether a vector remains active or can be automatically removed.

## Stage

Defined step in the delivery process (build, test, release). Conceptual checkpoint for quality assurance. Deployments target landscape partitions, not stages directly.

## Landscape

Logical grouping of multiple stages and deployment targets. Provides holistic view of systems, dependencies, and infrastructure. Enables consistent orchestration from development through production.

Stages promote across landscapes: DEV landscape -> TEST landscape -> PROD landscape (Internal -> Early -> Rest).

See also: [[Konfidence]]
