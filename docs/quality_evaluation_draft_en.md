# MCP Quality Grading Standard Draft (v0.1)

As the MCP community ecosystem continues to flourish, the number of MCP Servers is rapidly increasing. However, we have observed that many MCP Servers suffer from poor quality, mainly in the following aspects:

1. Significant usability, compatibility, and security challenges during configuration and usage, resulting in frustrating experiences.
2. Among MCP-compliant Hosts and Servers in the community, the implementation of the protocol is still at an early stage. Most only implement `Tool`, while support for `Prompt`, `Resource`, `Sampling`, etc., is extremely rare.

Given the various issues in this early stage of ecosystem development, this project aims to design a quality evaluation standard for MCP Servers and Hosts from a comprehensive perspective (including users and developers). The goal is to establish a tiered evaluation system to provide valuable guidance and infrastructure to promote a high-quality, sustainable MCP ecosystem.

## Scope

Applicable to all open-source or closed-source Servers that conform to the MCP protocol (including stdio / SSE / HTTP adaptations).

## Design Principles

| Principle                                | Key Points                                                                                                                                                                                                                                             |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1. User-Value-Oriented 🎯**            | - **Usability First**: Ensure core features run stably to solve real-world problems<br>- **Ease of Use**: Lower the learning curve and provide a friendly UX<br>- **Practical Focus**: Address actual use cases, avoid theoretical designs             |
| **2. Layered Progressive Evaluation 📈** | - **Baseline Gatekeeping**: Set a clear minimum quality bar<br>- **Tiered Advancement**: Progress from basic functionality to core capabilities to added value<br>- **Balanced Weighting**: Distribute weights reasonably to avoid overemphasis        |
| **3. Objective & Quantifiable 📊**       | - **Measurability**: Define concrete, quantifiable evaluation criteria<br>- **Consistency**: Enable similar scoring from different evaluators<br>- **Transparency**: Ensure the evaluation process is open, traceable, and reproducible                |
| **4. Ecosystem Sustainability 🌱**       | - **Long-Term Value**: Focus on maintainability and community building<br>- **Openness & Inclusion**: Encourage diverse technical approaches<br>- **Incentivize Innovation**: Reward technological innovation and ecosystem contributions              |
| **5. Practical Implementation ⚙️**       | - **Incremental Adoption**: Support iterative standard updates and smooth upgrades<br>- **Tool-Friendly**: Standards should support automation<br>- **Community Involvement**: Encourage community participation in defining and executing evaluations |
| **6. Security & Compliance 🔒**          | - **Security First**: Treat security as a non-negotiable baseline<br>- **Privacy Respect**: Protect user privacy and comply with regulations<br>- **Clear Responsibility**: Establish clear accountability and risk warnings                           |

## Server Certification Levels

| Badge | Level                  | Description                                              |
| ----- | ---------------------- | -------------------------------------------------------- |
| 💎    | **Diamond \[90,100]**  | Exceptional quality, innovation-driven, highly impactful |
| 🥇    | **Gold \[80,90)**      | Production-ready, performance-tuned, secure and reliable |
| 🥈    | **Silver \[65,80)**    | Feature-complete, well-tested, fully documented          |
| 🥉    | **Bronze \[60,65)**    | Basic functionality complete, well-documented            |
| 🏗️    | **Incubating \[0,60)** | Early-stage, exploratory, functionally incomplete        |

## Server Recommendation Levels

Based on the certification level, we provide the following usage guidance:

### 🟢 Trusted (Recommended)

- **Diamond (💎)**: Top recommendation, suitable for all production use cases
- **Gold (🥇)**: Highly recommended, production-safe
- **Silver (🥈)**: Recommended for most development and test environments

### 🟡 Use with Caution (Conditionally Recommended)

- **Bronze (🥉)**: Cautiously recommended for non-critical use cases

  - Suitable for personal or internal experimental projects
  - Carefully review documentation and known issues before use
  - Recommended for users with technical expertise

### 🔴 Not Recommended (Risk Requires Assessment)

- **Incubating (🏗️)**: Not suitable for production use, for learning or experimentation only

  - Features may be incomplete or unstable
  - Lack of sufficient testing or documentation
  - Potential security or compatibility risks
  - Intended for developers to explore or contribute

## Scoring System

> The scoring system adopts a three-layer evaluation framework:
>
> - L1 Baseline (50 pts): Determines whether the Server is usable. Any failure in this layer disqualifies the Server.
> - L2 Core (30 pts): Determines whether the Server is usable in production.
> - L3 Plus (20 pts): Assesses long-term value, ecosystem stickiness, and competitiveness.

### L1 Baseline (50 pts)

| Dimension                     | Weight | Focus Areas                                                                                                  | Typical Checks (translatable to checklists)                                                                                                                                                                                                                                     |
| ----------------------------- | ------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Protocol Conformance          | 20     | - Version consistency<br>- Robust error handling<br>- Capability negotiation                                 | - `protocolVersion` declaration matches implementation<br>- Proper Handshake/Error/Abort boundary handling<br>- `listChanged` must trigger `notifications/tools/list_changed`<br>- Runtime must honor negotiated capabilities<br>- HTTP SSE supports `Last-Event-ID` for resume |
| Backward Compatibility        | 8      | - Protocol fallback<br>- Versioning & governance                                                             | - Fallback to POST/SSE<br>- Follows SemVer<br>- Deprecated marked ≥1 version in advance<br>- SSE fallback on POST failure<br>- Complete Feature-Flag & Upgrade Guide                                                                                                            |
| Security & Compliance         | 12     | - Secure transport<br>- Tool/Prompt injection protection<br>- Side-effect declaration<br>- Origin validation | - HTTPS + OAuth 2.1<br>- Tool name/description injection-safe<br>- Side-effect declaration<br>- Prompt injection defense<br>- Origin check against DNS Rebinding<br>- Fake origins return 403/400                                                                               |
| Deployability & Compatibility | 10     | - Cross-platform deployability<br>- Startup and packaging readiness                                          | - Supported OS list<br>- CLI boot succeeds on first try<br>- Docker/Helm/source deployment supported<br>- Release notes include runtime requirements<br>- `uvx/npx` runs successfully once<br>- Official image is pullable and probe-healthy                                    |

### L2 Core (30 pts)

| Dimension                | Weight | Focus Areas                                                             | Typical Checks                                                                                                      |
| ------------------------ | ------ | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Performance & Efficiency | 10     | - Tool execution responsiveness                                         | - Average tool latency<br>- Load test results for latency                                                           |
| Tool Abstraction         | 10     | - Schema design friendliness<br>- Type safety<br>- Side-effect metadata | - Tool schema design is developer-friendly<br>- Uses JSON Schema/Zod<br>- Abstracts behavior, not just API wrappers |
| User Experience (UX)     | 10     | - Easy onboarding<br>- Clear error messages                             | - Zero-config startup<br>- Friendly CLI/GUI error messages with actionable hints                                    |

### L3 Plus (20 pts)

| Dimension                      | Weight | Focus Areas                        | Typical Checks                                                                                                   |
| ------------------------------ | ------ | ---------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Community Impact               | 4      | - Open source community engagement | - Star/fork growth<br>- Issue activity and response time                                                         |
| Documentation & Examples       | 5      | - Structure and practicality       | - Well-organized docs (config/start/use cases)<br>- End-to-end examples                                          |
| Code Quality & Maintainability | 5      | - Bug management and test coverage | - Bug presence<br>- Unit/integration coverage ≥ 70%<br>- Zero tolerance for critical bugs                        |
| Ecosystem Openness             | 4      | - API standardization              | - MCP coverage of APIs<br>- Check % of existing services MCP-ified                                               |
| Protocol Completeness          | 2      | - Sub-protocol support             | - Prompt/Tool/Resource implementation<br>- Full capability/notification support<br>- Sub-protocol coverage check |

## Evaluation Process & Methodology

> To be continued...

## 🤝 Contributing

We welcome community participation in improving this standard:

- 📝 **Standard Refinement**: Propose improvements and additions
- 🔍 **Evaluation Participation**: Join real-world project assessments
- 📚 **Documentation Contributions**: Help improve evaluation guides and best practices
- 🛠️ **Tooling Development**: Build automated evaluation tools

Let’s work together to build a high-quality MCP ecosystem!
