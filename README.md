- *CleanStart Container for Logstash Exporter**

Official Logstash Exporter container image optimized for enterprise environments. Includes comprehensive Prometheus metrics collection for Logstash instances and monitoring capabilities. Features security-hardened base image, minimal attack surface, and FIPS-compliant cryptographic modules. Supports both production deployments and development workflows with separate tagged versions. Includes Logstash exporter, metrics collection, and essential monitoring tools.

- *Key Features**
- Complete Logstash monitoring environment with metrics collection
- Optimized for cloud-native and microservices architectures

- *Common Use Cases**
- Building and deploying Logstash monitoring
- Cloud-native observability development

- *Pull Commands**
Download the runtime container images

```bash
docker pull cleanstart/logstash-exporter:latest
docker pull cleanstart/logstash-exporter:latest-dev
```

- *Interactive Development**
Start interactive session for development

```bash
docker run --rm -it --entrypoint /bin/sh cleanstart/logstash-exporter:latest-dev
```

- *Container Start**
Start the container
```bash
docker run --rm -it --name logstash-exporter-dev cleanstart/logstash-exporter:latest
```

- *Best Practices**
- Use specific image tags for production (avoid latest)
- Configure resource limits: memory and CPU constraints
- Enable read-only root filesystem when possible

- *Architecture Support**

- *Multi-Platform Images**

```bash
docker pull --platform linux/amd64 cleanstart/logstash-exporter:latest
docker pull --platform linux/arm64 cleanstart/logstash-exporter:latest
```

- *

###

## Resources

- **Official Documentation:** https://github.com/BobTheShoplifter/logstash-exporter
- **Provenance / SBOM / Signature:** https://images.cleanstart.com/images/logstash-exporter
- **Docker Hub:** https://hub.docker.com/r/cleanstart/logstash-exporter
- **CleanStart All Images:** https://images.cleanstart.com
- **CleanStart Community Images:** https://hub.docker.com/u/cleanstart

### Vulnerability Disclaimer

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

Security remains a shared responsibility: CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
