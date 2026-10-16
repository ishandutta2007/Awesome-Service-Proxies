# Awesome-Service-Proxies

# Top Service Proxies Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Layer 4/7 Load Balancing, Dynamic Service Discovery & Traffic Management*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Service Proxies**. These tools sit between clients and backend services — distributing traffic, terminating TLS, enforcing policies, and providing observability across bare metal, containers, and cloud environments.

**Examples** include HAProxy, NGINX, Traefik, Envoy, Kong, F5 BIG-IP, Citrix ADC, Kemp LoadMaster, AWS ALB, and Cloudflare (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, dynamic configuration, and transparent traffic management — ideal for platform engineers prioritizing control, avoiding vendor lock-in, and building infrastructure that scales from a single VPS to multi-cluster Kubernetes.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[F5 BIG-IP](https://www.f5.com/)**  
  Enterprise Application Delivery Controller (ADC) with advanced Layer 4-7 traffic management, WAF, DDoS mitigation, and global server load balancing (GSLB). Hardware and virtual editions available. **VE-200M starts at ~$6,146** with throughput capped at 0.2 Gbps [citation:7]. Best for large enterprises with dedicated network teams.

- **[Citrix ADC (NetScaler)](https://www.citrix.com/)**  
  Enterprise ADC with strong application acceleration, content switching, and security features. **VPX-200 starts at $15,000** with 0.2 Gbps throughput; **VPX-3000 at $36,000** supports 3 Gbps [citation:7]. Deep integration with Citrix virtualization stack.

- **[Kemp LoadMaster](https://kemptechnologies.com/)**  
  Cost-effective commercial load balancer with **Virtual LoadMaster 1G at $2,400** (0.5 Gbps) and **5G at $6,000** (3 Gbps) [citation:7]. Includes WAF, DDoS mitigation, and centralized management. Best for mid-market organizations wanting enterprise features at lower cost.

- **[AWS Application Load Balancer (ALB)](https://aws.amazon.com/elasticloadbalancing/)**  
  Fully managed Layer 7 load balancer for HTTP/HTTPS traffic with **path-based and host-based routing, WebSocket support, and native AWS WAF integration** [citation:18]. **$0.0225/hour base + $0.008 per LCU-hour**. Best for HTTP APIs and web apps in a single AWS region.

- **[AWS Network Load Balancer (NLB)](https://aws.amazon.com/elasticloadbalancing/)**  
  Fully managed Layer 4 load balancer for TCP/UDP traffic with **ultra-low latency and static IP addresses** [citation:18]. **$0.006 per NLCU-hour** — roughly 25% cheaper per capacity unit than ALB. Best for connection-heavy, latency-sensitive workloads.

- **[Cloudflare Load Balancing](https://www.cloudflare.com/)**  
  Global server load balancing with health checks, failover, and DDoS mitigation bundled with CDN and WAF. **Starts at $5/month per origin** — the cheapest managed option for multi-region failover [citation:8]. Best as a global steering layer in front of regional ALB/NLB deployments.

- **[NGINX Plus](https://www.nginx.com/)**  
  Commercial version of NGINX with **active health checks, live activity monitoring, and dynamic reconfiguration** not available in the open-source edition [citation:12]. Enterprise support and Nginx App Protect WAF.

## Open-Source GitHub Projects

- **[HAProxy](https://github.com/haproxy/haproxy)**  
  **The high-performance veteran** — battle-tested Layer 4/7 proxy known for low latency under heavy traffic, with **13+ load-balancing algorithms** including round-robin, least connections, and consistent hashing [citation:3]. **Runtime API and Data Plane API** enable dynamic backend updates without full reloads [citation:1]. In head-to-head Kubernetes Ingress benchmarking, **HAProxy handled ~42,000 requests/second — 2.2x faster than Envoy (18,500) and 3.6x faster than NGINX (11,700)** — with the lowest CPU usage and zero HTTP errors [citation:11]. **GPL-2.0 licensed**. The tradeoff is a steeper learning curve and no built-in certificate automation. Best for high-traffic sites and teams wanting fine control.

- **[NGINX](https://github.com/nginx/nginx)**  
  **The world's most popular web server and reverse proxy** — BSD-2-Clause licensed [citation:2]. Handles **HTTP/HTTPS, TCP/UDP, mail proxying, caching, and Layer 7 load balancing** with round-robin, least connections, and hash-based methods [citation:1][citation:2]. **Modular architecture** with filters for gzip, SSI, image transformation, and njs scripting. Supports **HTTP/3, HTTP/2, gRPC, and WebSocket** [citation:2]. Advanced active health checks and richer metrics sit in NGINX Plus [citation:1]. Best for teams already running NGINX who want one tool for serving and balancing.

- **[Traefik](https://github.com/traefik/traefik)**  
  **The cloud-native load balancer built for dynamic environments** — MIT licensed, **65,000+ GitHub stars** [citation:10][citation:14]. **Auto-discovers services from Docker, Kubernetes, Consul, etcd, and more** — routes appear and disappear as containers scale, with **no restarts required** [citation:4][citation:14]. **Automatic HTTPS via Let's Encrypt** (including wildcard certificates), circuit breakers, retries, and a clean web UI [citation:4]. **3.3 billion downloads** and strong Kubernetes integration [citation:14]. Tradeoff: lower raw throughput than tuned HAProxy, fewer low-level controls. Best for container-first teams that value automation.

- **[Envoy](https://github.com/envoyproxy/envoy)**  
  **The modern service mesh proxy and universal data plane** — Apache 2.0 licensed, CNCF graduated project [citation:5][citation:15]. **Originally built at Lyft** and used as the data plane in Istio, AWS App Mesh, and Gloo [citation:1][citation:5]. Features **HTTP/2, HTTP/3, gRPC, advanced traffic shaping, Wasm/Lua/Go/Rust extensibility, and deep L7 observability** [citation:5]. **Streaming-first architecture** now handles **AI/LLM traffic as first-class citizens** — token-aware rate limiting, provider fallback, and agentic workloads [citation:5]. Tradeoff: operational complexity and verbose configuration. Best for microservices, gRPC, and mesh edges.

- **[Kong Gateway OSS](https://github.com/Kong/kong)**  
  **The most popular open-source API gateway** — Apache 2.0 licensed [citation:6][citation:19]. **Built on NGINX and OpenResty** with LuaJIT for plugin extensibility [citation:9][citation:16]. Features **95+ plugins** for rate-limiting, authentication, transformations, and observability [citation:16]. **decK CLI** provides declarative GitOps configuration: `deck gateway dump` exports state, `deck gateway sync` applies it with diff preview [citation:19]. **Low latency <1ms and 50K+ transactions/second per node** [citation:16]. **Kong Enterprise** adds OIDC, RBAC, OPA, dev portal, and advanced analytics [citation:6][citation:16]. Best for API management where plugin ecosystem matters.

- **[Apache APISIX](https://github.com/apache/apisix)**  
  **Vendor-neutral API gateway under the Apache Software Foundation** — Apache 2.0 licensed [citation:9]. **Built on NGINX and LuaJIT** with **etcd-backed dynamic configuration** or standalone file mode [citation:9]. Plugin ecosystem spans **authentication (JWT, OIDC), traffic management (rate limiting, circuit breaking), observability (Prometheus, OpenTelemetry), and gRPC transcoding** [citation:9]. Supports **external plugin runners and WebAssembly** in addition to native Lua [citation:9]. Best for teams wanting community-governed API gateway without vendor control.

- **[Caddy](https://github.com/caddyserver/caddy)**  
  **Automatic HTTPS by default** — written in Go, MIT licensed. **The simplest reverse proxy to configure** with a Caddyfile that reads like English. **Automatic certificate provisioning and renewal** without extra tooling. Best for single-server setups and developers who want TLS handled for them.

### Additional Strong Open-Source Options

- **HAProxy Unified Gateway** — Free, open-source cloud-native routing with Kubernetes Gateway API integration [citation:3].
- **HAProxy Kubernetes Ingress Controller** — High-performance ingress with dynamic service discovery [citation:3][citation:11].
- **Nginx Proxy Manager** — Web UI for managing NGINX reverse proxies with SSL termination [citation:20].
- **SWAG (Secure Web Application Gateway)** — NGINX reverse proxy with built-in Certbot and fail2ban [citation:10][citation:20].
- **Zoraxy** — General-purpose HTTP reverse proxy and forwarding tool with WebUI [citation:10].
- **Varnish Cache** — Web application accelerator/caching HTTP reverse proxy [citation:10][citation:20].
- **Tyk Gateway** — MPL 2.0 licensed API gateway in Go with REST, GraphQL, and gRPC support [citation:19].
- **KrakenD Community Edition** — Stateless, high-performance gateway with Apache 2.0 license. Single Go binary, config-file driven, no database [citation:19].

**Frameworks for building custom systems**: Combine **HAProxy** for maximum throughput and fine-grained control, **Traefik** for automatic service discovery in containers, **Envoy** for service mesh and AI/LLM traffic management, **Kong** or **APISIX** for API gateway plugin ecosystems, and **Caddy** for simplest possible HTTPS reverse proxying — to build a service proxy layer tailored to your deployment shape and operational maturity.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Service proxies differ significantly in throughput, configuration complexity, and deployment model. **HAProxy leads on raw Kubernetes Ingress performance** — ~42,000 req/s in independent benchmarking, 2.2x faster than Envoy and 3.6x faster than NGINX [citation:11]. **Traefik excels at dynamic container environments** where manual route configuration doesn't scale [citation:1]. **Envoy is overkill for simple two-backend websites** but essential for microservices and service mesh [citation:1]. **NGINX Open Source lacks active health checks** — those require NGINX Plus [citation:1]. **Cloud-managed balancers (ALB, Cloudflare) eliminate maintenance** but add vendor dependency and per-request costs that climb with traffic [citation:8]. **Performance benchmarks are workload-dependent** — validate against your specific traffic patterns.
- Self-hosted open-source solutions require proper TLS certificate management, health check configuration, and monitoring of proxy performance and error rates.

---

**Made for platform engineers, DevOps teams, SREs, and developers building reliable service infrastructure.**  
Let's make service proxies more open, performant, and operationally simple.
