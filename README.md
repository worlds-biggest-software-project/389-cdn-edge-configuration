# CDN Edge Configuration

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> An open, AI-augmented control plane for deploying edge functions, traffic shaping, and DDoS protection across global points of presence.

CDN Edge Configuration is a unified platform for managing edge functions, cache rules, WAF policies, DDoS protection profiles, and traffic shaping logic across geographically distributed points of presence. It is designed for developers and platform engineers who need programmable edge behaviour with safe rollout, instant rollback, and per-PoP observability without being locked into a single proprietary CDN vendor.

---

## Why CDN Edge Configuration?

- **Vendor lock-in is severe.** Each major incumbent (Cloudflare Workers, Fastly Compute, AWS Lambda@Edge, Vercel, Akamai, Azure Front Door) implements proprietary APIs for edge state — KV stores, Durable Objects, EdgeKV — and code written for one platform typically requires substantial refactoring to run on another.
- **Configuration drift goes undetected.** No incumbent platform offers automatic consistency checking across all PoPs during deployment; partial propagation bugs are often discovered post-facto.
- **Cache invalidation remains a chronic pain point.** Surrogate key (cache tag) systems help but require manual application instrumentation.
- **L7 DDoS mitigation requires manual tuning.** Most platforms offer volumetric scrubbing, but behavioural anomaly detection and challenge mechanisms at the application layer demand bespoke configuration.
- **Closed control planes.** All six major incumbents are proprietary SaaS; there is no permissive open-source alternative for the control plane itself.

---

## Key Features

### Request Handling and Routing

- Request transformation, URL rewriting, and custom header injection at the edge
- Geolocation-based routing and dispatch
- A/B test assignment and personalisation before the cache layer
- Custom backend selection and request routing logic

### Cache Control

- TTL manipulation and cache bypass rules
- Surrogate key (cache tag) invalidation
- Predictable global purge for fine-grained URL patterns
- Cache hit and miss observability per PoP

### Deployment and Rollout

- Global propagation to all PoPs with detectable partial-propagation states
- Staged rollout and canary deployments (e.g. deploy to 1% of PoPs, then expand)
- Instant rollback to prior versions when issues are detected
- Configuration drift detection and continuous verification that all PoPs match intent

### Security at the Edge

- L7 DDoS mitigation with bot detection and challenge mechanisms
- WAF baseline (rate limiting, application-layer protection)
- Secure secret injection at deploy time (no hardcoded credentials)
- Optional dynamic secret rotation using short-lived OIDC tokens

### Observability

- Per-PoP metrics: cache hit rate, request volume, error rates, latency histograms
- Request-level logging with real-time streaming to external observability platforms
- Multi-region health probes for origin selection and failover

---

## AI-Native Advantage

AI augments edge configuration in ways that incumbents currently leave to manual tuning. The platform can analyse traffic patterns, cache hit ratios, and error signatures to recommend cache rules, TTLs, and routing logic. Behavioural models trained on baseline traffic flag deviations indicative of L7 application-layer attacks without manual rule authoring. Cache invalidation patterns can be inferred from API schemas or code analysis, reducing the burden of manual surrogate key definition. WAF and bot-detection policies can be synthesised from threat intelligence and observed traffic.

---

## Tech Stack & Deployment

The platform targets a programmable edge runtime supporting JavaScript/TypeScript and WebAssembly, aligning with WinterCG (Ecma TC55) standardisation efforts to reduce vendor lock-in. Edge functions run in lightweight isolates for sub-millisecond cold starts. The control plane supports CLI-first development workflows, GitHub-based CI/CD, environment-variable management, and progressive disclosure from simple request handlers to stateful edge compute. Deployment modes include self-hosted control planes and federation across multiple CDN providers, addressing the multi-cloud edge gap left by all incumbents.

---

## Market Context

The CDN and edge computing market is dominated by Cloudflare, Fastly, AWS CloudFront, Vercel, Akamai, and Azure Front Door — all proprietary SaaS offerings. AWS introduced flat-rate pricing bundling CDN, WAF, DDoS, and DNS in November 2025, signalling a shift toward predictable cost models. Azure's CDN market share fell to 10.3% in February 2026, down from 19.9% the prior year, indicating consolidation pressure. Primary buyers are platform engineering teams, SRE organisations, and security-conscious enterprises adopting zero-trust architectures.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed
open-source material with a compatible licence. Copyright infringement and licence
violations will not be tolerated and will result in immediate removal of the offending
contribution. If you are unsure whether a piece of code, text, or other material is
safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. See [discussion](#) for context.
