# Jaeger Components
- **Agent** is the component co-located with your application to gather the Jaeger trace data locally. It handles the connection and traffic control to the Collector (see below) as well as data enrichment.
- **Collector** is a centralized hub collecting traces from the various agents in the environment and sends for backend storage. The collector can run validations and enrichment on the spans.
- **Query** retrieves the traces and serves them over a UI.

# Installation tools for Jaeger
- Manually using kubectl
- Kubernetes Operator

# Helm:
`helm repo add jaegertracing https://jaegertracing.github.io/helm-charts'

\


TrioDownloaderGUI-DEV.dmg