# Standards & API Reference

> Project: CDN Edge Configuration · Generated: 2026-05-06

## Industry Standards & Specifications

### IETF / RFC Standards

**RFC 9111 — HTTP Caching**
- URL: https://datatracker.ietf.org/doc/html/rfc9111
- Defines the semantics of HTTP caches and the header fields that control cache behaviour (Cache-Control, Age, Expires, Pragma). Supersedes RFC 7234. Any CDN edge configuration tool must implement and expose these directives correctly.

**RFC 9213 — Targeted HTTP Cache Control**
- URL: https://datatracker.ietf.org/doc/html/rfc9213
- Defines a convention for response header fields that direct cache directives at specific caches or cache classes, including the CDN-Cache-Control header specifically targeting CDN caches. Essential for multi-tier cache hierarchies where origin, CDN, and browser caches have different desired TTLs.

**RFC 9110 — HTTP Semantics**
- URL: https://datatracker.ietf.org/doc/html/rfc9110
- The authoritative definition of HTTP semantics shared across HTTP/1.1, HTTP/2, and HTTP/3. Governs request methods, response codes, header field semantics, content negotiation, and conditional requests. Directly relevant to correct CDN behaviour for Vary, ETag, If-None-Match, and conditional caching.

**RFC 9211 — The Cache-Status HTTP Response Header Field**
- URL: https://datatracker.ietf.org/doc/rfc9211/
- Defines a standardised Cache-Status response header that CDNs and caching proxies can append to explain how they handled a request (hit, miss, stale, revalidated, etc.). Authored by engineers at Fastly. Important for observability and debugging of multi-layer CDN configurations.

**RFC 8941 — Structured Field Values for HTTP**
- URL: https://datatracker.ietf.org/doc/html/rfc8941
- Defines a standardised syntax and parsing model for HTTP header field values using lists, dictionaries, and items. Underpins newer HTTP extensions including Cache-Status and CDN-Cache-Control; any tooling that parses or generates these headers should conform to this specification.

**RFC 6707 — CDNI Problem Statement**
- URL: https://datatracker.ietf.org/doc/html/rfc6707
- Articulates the motivations for CDN Interconnection (CDNI): enabling standalone CDNs to interoperate as an open content delivery infrastructure. Provides the conceptual foundation for the broader CDNI RFC family.

**RFC 7336 — Framework for Content Distribution Network Interconnection (CDNI)**
- URL: https://datatracker.ietf.org/doc/rfc7336/
- Describes the core CDNI architecture and the interfaces between upstream and downstream CDNs. Relevant when a CDN edge configuration platform must support multi-CDN deployments or CDN failover.

**RFC 7337 — CDNI Requirements**
- URL: https://datatracker.ietf.org/doc/html/rfc7337
- Enumerates the functional requirements for CDNI, covering the Control Interface (CI), Request Routing interface, and trigger operations for pre-positioning, revalidation, and purge.

**RFC 8006 — CDNI Metadata**
- URL: https://datatracker.ietf.org/doc/html/rfc8006
- Defines the Metadata Interface allowing interconnected CDNs to exchange content distribution metadata, providing a downstream CDN with sufficient information to serve content on behalf of an upstream CDN.

**RFC 8007 — CDNI Control Interface / Triggers**
- URL: https://datatracker.ietf.org/doc/html/rfc8007
- Specifies the control interface by which an upstream CDN instructs a downstream CDN to pre-position, revalidate, or purge metadata and content, with TLS required for transport. Directly applicable to cache invalidation API design.

**RFC 8804 — CDNI Request Routing Extensions**
- URL: https://datatracker.ietf.org/doc/html/rfc8804
- Extends the CDNI Metadata and Footprint & Capabilities Advertisement interfaces. Covers the Open Caching use case where a commercial CDN acts as upstream and an ISP caching layer acts as downstream.

**IETF Draft — CDNI Edge Control Metadata**
- URL: https://datatracker.ietf.org/doc/draft-ietf-cdni-edge-control-metadata/
- Active draft (latest version: 04, 2025) defining configuration metadata objects for controlling edge access including CORS rules, response body compression, client connection timeouts, and access control at the edge. Directly relevant to the configuration model of an AI-native CDN configuration tool.

**IETF Draft — CDNI Cache Control Metadata**
- URL: https://datatracker.ietf.org/doc/html/draft-ietf-cdni-cache-control-metadata-05
- Active 2025 Internet-Draft addressing fine-grained control over downstream CDN caching, including scenarios where overriding or adjusting upstream cache-control headers is desirable.

### W3C Standards

**W3C Edge Architecture Specification 1.0**
- URL: https://www.w3.org/TR/edge-arch/
- W3C specification describing a framework for distributing HTTP content via surrogates (reverse proxies and CDN edge nodes), including the Surrogate-Control header and its directives. Underpins the Edge Side Includes (ESI) markup language.

**W3C Edge Side Includes (ESI)**
- URL: https://www.w3.org/TR/esi-lang/ (submitted to W3C August 2001; widely implemented)
- Defines an XML markup language inserted in HTML content that instructs CDN/surrogate nodes to assemble dynamic page fragments with different cache TTLs. Supported by Akamai, Fastly (via Varnish VCL), and Varnish Cache; relevant when designing CDN configuration around fragment-level caching.

### Data Model & API Specifications

**OpenAPI 3.1**
- URL: https://spec.openapis.org/oas/v3.1.0
- The standard format for describing REST APIs. All major CDN providers (Cloudflare, Fastly, Akamai) publish OpenAPI or Swagger specifications for their configuration APIs. An AI-native CDN configuration platform should expose an OpenAPI 3.1-compliant API.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/specification.html
- Used to validate CDN configuration payloads (edge rules, cache policies, WAF rule sets). Both Cloudflare and Fastly use JSON-based configuration formats that can be described and validated with JSON Schema.

**WebAssembly (Wasm) Core Specification 2.0**
- URL: https://webassembly.github.io/spec/core/
- The binary instruction format targeted by Fastly Compute and Cloudflare Workers (via compilation from Rust, C, Go, JavaScript). Relevant to any tooling that packages and deploys edge function artefacts.

**WinterCG (Web-interoperable Runtimes Community Group) — Minimum Common Web Platform API**
- URL: https://wintercg.org/
- A W3C Community Group establishing a common API baseline for server-side JavaScript runtimes including Cloudflare Workers, Deno Deploy, and Fastly Compute. Relevant for portable edge function abstractions.

### Security & Authentication Standards

**OAuth 2.0 (RFC 6749) and OAuth 2.0 Bearer Tokens (RFC 6750)**
- URL: https://datatracker.ietf.org/doc/html/rfc6749
- The dominant authorisation framework used by CDN management APIs (Cloudflare, Fastly, Akamai all support OAuth 2.0 client credentials for machine-to-machine API access).

**OpenID Connect 1.0**
- URL: https://openid.net/specs/openid-connect-core-1_0.html
- Identity layer on top of OAuth 2.0; used for operator authentication to CDN management dashboards and CLI tools.

**ISO/IEC 27001:2022 — Information Security Management Systems**
- URL: https://www.iso.org/standard/82875.html
- The primary information security management standard. Annex A 5.23 (new in 2022) specifically addresses information security for use of cloud services, including data residency, encryption, and sub-processor transparency — all relevant to CDN edge configuration storing configuration data and processing end-user traffic.

**GDPR (EU) 2016/679**
- URL: https://gdpr.eu/
- The EU data protection regulation. CDN edge configuration tools must support geo-restriction rules, data residency controls, and audit logging to enable operators to demonstrate GDPR compliance. Cloudflare's Customer Metadata Boundary and regional data isolation features are direct responses to GDPR requirements.

**OWASP Top 10 & OWASP API Security Top 10**
- URL: https://owasp.org/www-project-top-ten/ and https://owasp.org/www-project-api-security/
- Industry-standard vulnerability catalogues. CDN WAF configuration tools commonly map rulesets to OWASP categories. An AI-native configuration platform should surface OWASP-aligned recommendations when generating WAF and security policies.

**TLS 1.3 (RFC 8446)**
- URL: https://datatracker.ietf.org/doc/html/rfc8446
- The current TLS standard required at CDN edge for HTTPS termination and origin connections. Relevant to configuration options around minimum TLS version, cipher suites, mTLS for viewer and origin authentication, and HSTS enforcement.

**mTLS / Client Certificate Authentication (RFC 8705)**
- URL: https://datatracker.ietf.org/doc/html/rfc8705
- OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens. Relevant to CDN features like AWS CloudFront viewer mTLS (introduced 2026) that require client certificate validation at the edge.

---

## Similar Products — Developer Documentation & APIs

### Cloudflare (Workers, Rules, CDN)

- **Description:** Global CDN and edge computing platform with 300+ PoPs. Offers configurable cache rules, WAF, DDoS protection, edge functions (Workers), and traffic shaping via a unified Rulesets API.
- **API Documentation:** https://developers.cloudflare.com/api/
- **Configuration Rules API:** https://developers.cloudflare.com/rules/configuration-rules/create-api/
- **SDKs/Libraries:** Wrangler CLI (JavaScript/TypeScript) — https://developers.cloudflare.com/workers/wrangler/; Cloudflare Terraform Provider — https://github.com/cloudflare/terraform-provider-cloudflare
- **Developer Guide:** https://developers.cloudflare.com/workers/
- **Standards:** REST/JSON, OpenAPI; Ruleset API uses JSON-based rule expressions
- **Authentication:** API token (Bearer), OAuth 2.0 client credentials for automation

### Fastly (CDN, Compute, VCL)

- **Description:** CDN and edge computing platform. Offers a VCL-based full-site delivery configuration model and a WebAssembly-first Compute platform. Config Stores provide edge key-value state for dynamic configuration.
- **API Documentation:** https://www.fastly.com/documentation/reference/
- **SDKs/Libraries:** Fastly CLI (Rust, Go, JavaScript SDKs for Compute) — https://www.fastly.com/documentation/guides/compute/; Fastly Terraform module
- **Developer Guide:** https://www.fastly.com/documentation/guides/compute/getting-started-with-compute/; VCL guide — https://www.fastly.com/documentation/guides/full-site-delivery/custom-vcl/developer-guide-using/
- **Standards:** REST/JSON; VCL (Varnish Configuration Language derivative)
- **Authentication:** API token (Bearer); Fastly API tokens are scoped by service and permission level

### AWS CloudFront

- **Description:** Amazon's globally distributed CDN, deeply integrated with the AWS ecosystem. Supports Lambda@Edge and CloudFront Functions for request/response manipulation; viewer mTLS added 2026.
- **API Documentation:** https://docs.aws.amazon.com/cloudfront/latest/APIReference/
- **SDKs/Libraries:** AWS SDK (JavaScript, Python, Java, Go, PHP, .NET, Ruby) — https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/CloudFront.html; AWS CDK — https://docs.aws.amazon.com/cdk/api/v2/python/aws_cdk.aws_cloudfront/README.html
- **Developer Guide:** https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html; CloudFront Functions — https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-functions.html
- **Standards:** REST/XML and REST/JSON; AWS CloudFormation template format — https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-cloudfront-distribution-distributionconfig.html
- **Authentication:** AWS SigV4 request signing via IAM credentials and roles

### Akamai (EdgeWorkers, Property Manager API)

- **Description:** Carrier-grade CDN and security platform with the largest global edge network. Property Manager defines delivery configuration as a rule tree; EdgeWorkers enables serverless edge logic.
- **API Documentation:** https://techdocs.akamai.com/developer/docs/edgegrid
- **Property Manager API (PAPI):** https://techdocs.akamai.com/property-mgr/reference/api-get-started
- **SDKs/Libraries:** EdgeGrid SDKs (Go — https://github.com/akamai/AkamaiOPEN-edgegrid-golang; Node — https://github.com/akamai/AkamaiOPEN-edgegrid-node); Akamai Terraform provider
- **Developer Guide:** https://techdocs.akamai.com/developer/docs/authenticate-with-edgegrid
- **Standards:** REST/JSON; proprietary EdgeGrid authentication protocol (HMAC-SHA256 request signing)
- **Authentication:** EdgeGrid — HMAC-SHA256 signature over request components using credentials from an `.edgerc` file; permission scopes set per API client

### bunny.net (CDN, Edge Rules, Edge Scripting)

- **Description:** Cost-efficient CDN with a simple Edge Rules system for cache, routing, security, and redirect configuration. Introduced Edge Scripting (JavaScript-based) in 2024 for programmable edge logic.
- **API Documentation:** https://docs.bunny.net/cdn/edge-rules
- **SDKs/Libraries:** REST API; Bunny Launcher CLI for Edge Scripting
- **Developer Guide:** https://bunny.net/blog/introducing-the-new-edge-rules/; Edge Scripting — https://bunny.net/blog/introducing-bunny-edge-scripting-a-better-way-to-build-and-deploy-applications-at-the-edge/
- **Standards:** REST/JSON; Edge Rule configuration mirrors the API JSON format
- **Authentication:** API key (Bearer token per pull zone or account)

### Google Cloud CDN + Cloud Armor

- **Description:** Google's CDN integrated with its global load balancer. Cloud Armor provides WAF and edge security policies that apply to both cache hits and misses at the edge — closing a gap that standard backend-only WAF policies leave open.
- **API Documentation:** https://docs.cloud.google.com/cdn/docs; Cloud Armor — https://docs.cloud.google.com/armor/docs
- **SDKs/Libraries:** Google Cloud SDK (`gcloud compute backend-services`, `gcloud compute backend-buckets`); client libraries in Python, Go, Java, Node.js, Ruby
- **Developer Guide:** https://docs.cloud.google.com/architecture/deploy-programmable-gfe-cloud-armor-lb-cdn; Edge security policies — https://docs.cloud.google.com/armor/docs/configure-security-policies
- **Standards:** REST/JSON; Google Cloud resource model; Infrastructure-as-Code via Terraform google provider
- **Authentication:** OAuth 2.0 (service account credentials); Application Default Credentials (ADC)

### Vercel Edge Middleware

- **Description:** Next.js-native edge middleware that intercepts requests before the cache. Runs on the WinterCG-compatible Edge Runtime. Primarily targeted at Next.js and framework-native edge configuration.
- **API Documentation:** https://vercel.com/docs/routing-middleware
- **SDKs/Libraries:** `@vercel/edge` package; Vercel CLI; integrated with Next.js App Router
- **Developer Guide:** https://vercel.com/docs/routing-middleware
- **Standards:** WinterCG Minimum Common Web Platform API; TypeScript-first; configuration via `middleware.ts` and `vercel.json`
- **Authentication:** Vercel API tokens; OAuth 2.0 for third-party integrations via Vercel Marketplace

---

## Infrastructure-as-Code Provider References

| Provider | Registry URL | Notes |
|---|---|---|
| Cloudflare Terraform Provider | https://registry.terraform.io/providers/cloudflare/cloudflare/latest | Official; manages zones, rules, Workers, WAF |
| Fastly Terraform Module | https://registry.terraform.io/providers/fastly/fastly/latest | Official; manages services, domains, backends, VCL snippets |
| AWS CloudFront (hashicorp/aws) | https://registry.terraform.io/providers/hashicorp/aws/latest | Manages distributions, CloudFront Functions, policies |
| Akamai Terraform Provider | https://registry.terraform.io/providers/akamai/akamai/latest | Official; manages properties, EdgeWorkers, security configs |
| Google Cloud Terraform Provider | https://registry.terraform.io/providers/hashicorp/google/latest | Manages backend services, CDN policies, Cloud Armor |

---

## Notes

- **WinterCG compatibility** is the key emerging portability standard for edge functions. Tools that generate or manage edge functions should target WinterCG APIs to maximise compatibility across Cloudflare Workers, Fastly Compute, Deno Deploy, and future runtimes.
- **RFC 9213 (CDN-Cache-Control)** is seeing growing adoption but is not yet universally supported; Cloudflare and Fastly support it, while AWS CloudFront relies on its own cache policy configuration model rather than this header.
- **Akamai EdgeGrid** is the only major CDN authentication scheme that departs significantly from OAuth/API-key patterns. Any tool integrating with Akamai must implement the HMAC-SHA256 EdgeGrid signing algorithm.
- **CDNI Edge Control Metadata drafts** (especially `draft-ietf-cdni-edge-control-metadata`) are the closest thing to a vendor-neutral standard for edge configuration metadata, but they remain in draft status as of 2026 and have limited implementation outside open-caching/ISP deployments.
- **ESI (Edge Side Includes)** is legacy but still in use in enterprise contexts (especially Akamai). Modern alternatives favour component-level HTTP streaming and React Server Components over ESI fragment assembly.
