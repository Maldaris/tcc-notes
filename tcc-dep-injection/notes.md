## Dependency Injection

### What is?
  - Methodology that does inversion of control for dependencies, by passing a implementation of a service to the client

### What do?
  - Implements an interface to provide functionality without the client needing implementation-specific knowledge

### How Use?
  - MVC Model
  - In the controller, logic should be extracted to a service
  - Services should handle any sort of DAL or BL operations, and should be transparent to the controller.
  - Essentially: Make your controller exclusively wiring to the Buisness layer &amp; validating input/sanitization
  - Services should implement an interface
    - Interface should be the only reference to the service; if you need a implementation specific call, revisit your design.
    - Interfaces should be robust but agnostic.

### Benefits
  - Allows for casual swapping of services on a need-basis
  - Useful for templated applications &amp; and services
  - Useful if unified views are required, but buisness logic &amp; Data Access Layer implementation might change/scale
  - Offers high flexibility to change implementation to meet new techniques/services/libraries etc.
 
