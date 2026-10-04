# 02 — MuleSoft Fundamentals

## Slide 1 — What is MuleSoft?
**Answer:** MuleSoft is an integration platform used to connect applications, APIs, data and systems. In production support, the important part is understanding how an event travels through Mule and where failures can occur.

## Slide 2 — What is Mule 4?
**Answer:** Mule 4 is the runtime used to execute Mule applications. A Mule application contains flows, processors, connectors, transformations and error-handling logic.

## Slide 3 — What is a Mule Event?
**Answer:** A Mule event carries the **payload, attributes and variables** through processing. The payload is the main business data; attributes describe metadata about the message; variables hold supporting state.

## Slide 4 — Payload vs Attributes
**Answer:** The payload is the current message content being processed. Attributes contain metadata such as HTTP method, headers or listener information. A transformation can replace the payload while attributes remain associated with the event.

## Slide 5 — What are Variables?
**Answer:** Variables store values needed later in the flow, such as correlation-related data, calculated values or intermediate business information. Avoid storing unnecessarily large objects because they can increase memory pressure.

## Slide 6 — Flow vs Sub-flow vs Private Flow
**Answer:** A flow can have a source and execute independently. A sub-flow is reusable processing without its own event source and does not have its own error handler. A private flow is reusable and can contain its own error-handling behavior.

## Slide 7 — What is Flow Reference?
**Answer:** Flow Reference transfers processing to another flow/sub-flow and then returns control to the caller according to Mule's flow semantics. It is useful for reusable business or technical processing.

## Slide 8 — What is a Connector?
**Answer:** A connector provides integration with an external protocol or system, such as HTTP, Database, SFTP, Salesforce or messaging systems. When troubleshooting, identify whether the failure is in Mule configuration, network/security or the external system.

## Slide 9 — What is RAML?
**Answer:** RAML is an API modeling language used to describe resources, methods, parameters, request/response structures and examples. It defines the API contract that consumers and implementers can work from.

## Slide 10 — What is APIkit?
**Answer:** APIkit helps implement APIs from an API specification by providing routing and API implementation support. In troubleshooting, verify that the deployed API path, listener, base path and APIkit routing match the expected contract.

## Slide 11 — What is Runtime Manager?
**Answer:** Runtime Manager provides operational visibility and management for Mule applications, including deployments, application status and logs. It is commonly one of the first places an L2 support engineer checks during an incident.

## Slide 12 — What is CloudHub?
**Answer:** CloudHub is MuleSoft-managed application hosting. For support, validate application state, runtime logs, workers/replicas, configuration, listener availability and downstream connectivity.

## Slide 13 — What is Runtime Fabric?
**Answer:** Runtime Fabric allows Mule applications to run on infrastructure controlled by the organization, commonly with Kubernetes-based infrastructure. Troubleshooting may therefore involve both Mule runtime behavior and platform health.

## Slide 14 — What is a Worker?
**Answer:** A worker or execution instance runs the Mule application. Additional capacity can improve throughput or availability, but scaling cannot fix a bad query, unavailable dependency, incorrect configuration or poison message.

## Slide 15 — What is a vCore?
**Answer:** A vCore represents a unit of Mule runtime compute capacity. When resource pressure occurs, correlate it with traffic, payload size, transformation complexity, concurrency, recent deployments and downstream latency.

## Slide 16 — Production Interview Takeaway
**Answer:** For fundamentals, do not stop at definitions. Explain how the concept behaves in production, what evidence you would check during an incident, and how you would safely restore service.
