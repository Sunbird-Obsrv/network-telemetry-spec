## Reference Implementation Design

According to the network telemetry specification, all network participants (NPs) must transmit API transactions and metric data to the network facilitator. 
NPs are responsible for implementing the necessary mechanisms into their systems to produce and share this data to the facilitator, adhering to the SLAs and guidelines established within the network.

- **API Transactions Data:** NPs are required to create Open Telemetry SPANs for each API request and response they initiate. These SPANs should be constructed using API payloads and HTTP response information, following the open network telemetry specifications and the network specific extensions & policies.
- **Business & Operational Metrics:** NPs must generate Open Telemetry METRICs based on the definition, granularity, and frequency outlined in the metrics registry. NPs are required to perform computations or aggregations on raw data to produce the metric information.

Additionally, NPs may generate LOG events for internal use. The implementation and maintenance of the telemetry services and components may impose additional overheads on the NPs. Hence, the proposed reference architecture aims to empower NPs to generate telemetry data with minimal effort on their part.

<img width="1034" alt="ref-high-level-impl-design" src="https://github.com/maheshkumargangula/network-telemetry-spec/assets/6985261/3aaaf111-c874-4aac-8f26-e1991cb87401">

The network and TSP ecosystem can offer solutions that NPs can integrate into their systems and configure to produce telemetry data according to specified requirements. 
These solutions may also offer supplementary advantages and add value to NPs through data utilization. The reference architecture suggests the following components within the network ecosystem for end-to-end observability.

### Open Telemetry SDK

The Open Telemetry SDK needs to be a lightweight library that can be integrated into various systems. 
Its primary function is to take API payload and response data as input and produce the following outputs:
- API events in the form of OTel SPANs
- Audit events in the form of OTel LOGs

It should also facilitate the configuration of multiple endpoints for dispatching API events and Audit events, along with the raw API data. Typically, it's configured to dispatch API events to a network facilitator observability infrastructure while routing audit events and raw API data to either a local data platform or a micro-observability instance. 
These endpoints can then generate and share the necessary metrics as required.

> [!NOTE]
> An open-source JavaScript SDK (for Beckn networks) is presently in the works and is set to be released on both the sunbird-obsrv GitHub and npm repositories.

### Metrics Registry

The metrics registry has to function as an electronic registry at the network level containing a list of metrics to be produced by network participants and shared with the network facilitator. 
The metric definition comprises of the following details:
- Description of the metric, including its name, a unique code, and its category
- Status of the metric, indicating whether it is in draft, live, or retired
- Definition of the metric, in a human-readable manner and optionally in a machine-readable format based on the metric type
- Granularity of the metric and its generation frequency
- Agreed-upon SLAs for the metric
- Participant Criteria outlining the list of participants or criteria to ascertain who should generate the metric

Additionally, the registry has to be designed to facilitate workflows, allowing network entities to propose, review, and either accept or reject metrics for inclusion. 
This process ensures that the metrics registry reflects the changing needs and priorities of the network, promoting transparency and collaboration among its participants.

### N/W Facilitator Observability Infra

The Network facilitator observability infrastructure acts as the primary hub for enhancing network observability in addition to providing various data-driven benefits to the entire network. 
This infrastructure should possess the following capabilities:
- Collect API events and Metrics from all network participants. Process and store the ingested data.
- Enable network observability for the facilitator to monitor network health, compliance, fraud, and irregularities.
- Output network health information, anonymized and aggregated business metrics, and publicly accessible open datasets.
- Notify participants about significant events such as downtimes, etc.

<img width="1043" alt="network-faci-obsrv-infra" src="https://github.com/maheshkumargangula/network-telemetry-spec/assets/6985261/b6ace5e3-926b-4f77-a41e-835794bd2922">


The infrastructure should have the following components:
- Data Input API and Data In Connectors: These enable data exchange from network participants through various methods. Some participants may opt to transmit data through the API, while others may prefer sharing data that the infrastructure retrieves using connectors.
- An extensible data pipeline capable of supporting diverse data processing tasks such as cleansing, transformations, and processors. Additionally, it should be able to deploy and execute network specific transformers and processors.
- Storage capable of storing different data formats and supporting multiple querying modes.
- Output interfaces for data retrieval through APIs, event notifications, and the capability to access datasets through data exhausts functionalities.

### Micro Observability

A NP specific micro-observability system is essential for calculating metrics as outlined in the metrics registry and sending them to the network facilitator. The micro-observability system, alongside the telemetry SDK, is needed due to the requirement for a storage and query system supporting aggregations for metric computation. The SDK is supposed to be only a lightweight library without any storage or other intricate components. 
However, the micro-observability system can integrate the telemetry SDK within itself, serving as a unified interface for all telemetry requirements of a Network Participant.

While the primary function of a "Micro" Observability system is metric computation, it can be expanded to offer various data-driven features for Network Participants.

<img width="1047" alt="capabilities-mirco-obsrv-sys" src="https://github.com/maheshkumargangula/network-telemetry-spec/assets/6985261/47c4f2aa-cbc4-41e1-8a3f-ea70c303acc1">

Either TSPs or the network facilitator itself can develop and provide the micro-observability solution with the above mentioned capabilities and more to the network participants.





