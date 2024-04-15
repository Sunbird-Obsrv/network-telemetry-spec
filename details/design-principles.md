## Design Principles

Following are some of the key design principles in defining the network telemetry specification:
1. **Standardized events** - A standard event spec ensures a data first design principle with API evolvability, interoperable, correlatable data across the network, no lockin with data service providers, standardization of data sharing APIs and access control policies and enable sharing of only aggregated metric/summary data.
2. **Adopt OpenTelemetry Protocol** - Adopt the open telemetry protocol to ensure that we ride on the global adoption wave and there would be many tools that can be integrated with OpenTelemetry.
3. **No PII & Business Sensitive data** - Ensure that sensitive business-critical and personal data is neither captured nor shared, thereby addressing any privacy and unfair advantage concerns among network participants
Extensible telemetry specification - Enable capture of additional network participant specific data (non PII). This would ensure that the data producers can evolve without any impact to downstream data consumers
4. **Enable 5 pillars of data observability** - Enable network observers to derive qualitative data observability metrics like quality, lineage, schema, freshness and volume.
