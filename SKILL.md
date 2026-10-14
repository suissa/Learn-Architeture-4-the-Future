<!-- IMPORTANT: Replace every occurrence of "{linguagem-tal}" with the target implementation language before using this skill. -->

# SKILL — Implementing the Future Architecture in {linguagem-tal}

## Purpose

This skill defines how to implement a future-proof architecture whose primary property is continuous evolution under evidence. The implementation language is intentionally abstract: the architecture is defined by behavior, invariants, constraints, contracts, evidence and acceptance criteria, never by a particular language mechanism.

The implementation MUST preserve the architectural properties described in `docs/{nome-conceito}/README.md` for every concept listed in the root README.

## Core rule

Do not encode the architecture as a fixed collection of components. Encode stable invariants and contracts, while allowing implementations, policies, topology, resource allocation and generated behavior to change when evidence demonstrates that a change is safe and beneficial.

The system MUST distinguish:

- immutable safety and integrity invariants;
- evolvable policies and implementations;
- observed facts and inferred hypotheses;
- proposed changes and accepted changes;
- runtime state and durable knowledge;
- recovery actions and architectural evolution.

## Required architectural properties

The implementation MUST support, as first-class architectural concerns:

1. Generative architecture.
2. Adaptive architecture.
3. Generic architecture.
4. Evolutionary architecture.
5. Scalable architecture.
6. Antifragile architecture.
7. Self-healing architecture.
8. Polychromatic Language & Data Planes.
9. Syntropic architecture.
10. Autopoietic architecture.

These properties are not documentation labels. Each MUST have executable validation evidence.

## Invariants

The following invariants MUST hold regardless of implementation language, topology or deployment size.

### Safety invariants

- No generated or evolved behavior may bypass authorization boundaries.
- No experiment may intentionally affect an uncontrolled external target.
- No autonomous change may disable its own safety, rollback or observation mechanisms.
- Security-critical policy changes require explicit acceptance according to the configured governance level.
- Secrets and sensitive credentials MUST NOT be emitted into telemetry, test evidence or generated artifacts.
- Destructive experiments MUST have an enforceable termination condition.

### Data invariants

- Authoritative data MUST have a single explicitly defined authority for each mutation domain.
- A failed mutation MUST NOT be represented as successfully committed state.
- State transitions MUST be deterministic with respect to the same input, prior state and declared external observations, unless nondeterminism is explicitly part of the contract.
- Evolution MUST preserve data integrity and declared consistency guarantees.

### Contract invariants

- Every externally observable behavior MUST have a contract.
- Every contract MUST define valid, invalid, boundary and failure behavior where applicable.
- Backward compatibility MUST be preserved unless a versioned migration contract explicitly permits a breaking change.
- Unknown input MUST result in a defined failure or recovery behavior, never undefined execution.

### Evolution invariants

- Every proposed evolution MUST have a reason, evidence, expected benefit and rollback strategy.
- A change MUST be evaluated against the complete validation pipeline before promotion.
- The system MUST retain enough evidence to explain why an evolution was accepted, rejected or reverted.
- An optimization MUST NOT be accepted solely because one metric improved; required guardrails MUST remain within their constraints.

### Observability invariants

- Every test scenario MUST produce machine-readable evidence.
- Evidence MUST identify scenario, inputs, configuration, version, timestamp, outcome and relevant measurements.
- Metrics MUST distinguish observation from inference.
- Predictions MUST carry an uncertainty/confidence representation whenever the underlying method supports it.

## Constraints

The implementation MUST define explicit constraints for:

- CPU, memory, storage, network and connection budgets;
- request rate and concurrency;
- queue depth and backlog;
- latency and error-rate objectives;
- dependency failure domains;
- experiment duration;
- maximum blast radius;
- maximum autonomous change rate;
- rollback time;
- data retention for evidence;
- security and authorization boundaries;
- acceptable cost envelope.

Constraints MUST be externally configurable and versioned. Hard safety constraints MUST be enforceable independently from optimization logic.

## Evolution loop

The reference lifecycle is:

`Observe → Model → Generate → Experiment → Measure → Infer → Propose → Validate → Accept/Reject → Learn`

The loop MUST be able to operate continuously, but autonomous promotion MUST remain bounded by invariants and acceptance criteria.

The system SHOULD maintain a knowledge model containing:

- observed behavior;
- discovered boundaries;
- failure modes;
- successful recovery paths;
- performance envelopes;
- dependency relationships;
- scenario coverage;
- rejected hypotheses;
- accepted evolutions;
- regressions and reversions.

## Universal scenario generation

The validation system MUST generate scenarios across:

- nominal behavior;
- boundary values;
- invalid values;
- missing values;
- malformed values;
- extreme values;
- concurrent requests;
- sequential state transitions;
- dependency degradation;
- dependency failure;
- resource exhaustion;
- network degradation;
- security abuse;
- recovery and restart;
- configuration changes;
- version changes;
- combinations of high-risk dimensions.

Exhaustive enumeration MAY be used for small finite domains. For large or infinite domains, the implementation MUST use bounded exhaustive sampling, property-based generation, combinatorial coverage, boundary exploration, mutation/fuzzing and adaptive search.

## Ten-year accelerated validation

The official validation model MUST simulate ten years of operation.

Simulation time is accelerated so that:

`10 seconds = 1 simulated day`

Therefore:

- 3650 simulated days represent approximately ten years;
- the simulation MUST preserve deterministic control over simulated time;
- tests MUST be able to inspect behavior at day, month, year and decade boundaries;
- long-term state accumulation MUST be included where the architecture has persistent state;
- scheduled maintenance, rotations, retention, growth and degradation MUST be represented when applicable.

The ten-year simulation is a validation horizon, not a requirement to literally wait ten years.

## Official evidence commands

The architecture MUST expose the following logical test commands. Their implementation is language- and tool-independent:

- `run:unitary:evidence`
- `run:bdd:evidence`
- `run:load:evidence`
- `run:stress:evidence`
- `run:chaos:evidence`
- `run:security:evidence`
- `run:benchmark:evidence`
- `run:pipeline:evidence`

Each command MUST return a process status suitable for automation and MUST emit structured evidence.

`run:pipeline:evidence` MUST execute the complete validation sequence and MUST NOT silently omit a required stage.

The test commands MUST be declared in `config.yml` so that the architecture does not assume a particular test framework.

## Required test semantics

### Unit evidence

Validate individual behaviors, invariants, contracts, transformations and failure handling.

### BDD evidence

Validate externally observable behavior using scenarios expressed in business/domain terms. Scenarios MUST include successful, boundary, invalid and recovery paths.

### Load evidence

Measure behavior under expected and progressively increasing sustained demand. Record throughput, latency distribution, errors, saturation signals and recovery.

### Stress evidence

Push the system beyond expected operating conditions in a controlled environment to identify degradation and failure thresholds.

### Chaos evidence

Inject controlled faults into dependencies, resources, network paths and runtime conditions. Validate graceful degradation, recovery and invariant preservation.

### Security evidence

Validate authentication, authorization, isolation, input handling, secret handling, abuse resistance, dependency trust boundaries and security invariants.

### Benchmark evidence

Measure performance against a stable baseline. Benchmark changes MUST be comparable across versions and configurations.

### Pipeline evidence

Execute all required evidence stages, aggregate their results, evaluate acceptance criteria and produce one auditable result.

## Real-time TUI executor contract

A separate TUI skill MUST implement the official terminal executor. The TUI is an orchestration and evidence-visualization layer, not the source of truth for test semantics.

The executor MUST:

- load `config.yml`;
- expose the eight official commands;
- execute configured commands without changing their semantics;
- stream stdout/stderr and structured events in real time;
- show test status, progress, duration, throughput, failures and evidence summaries;
- support cancellation;
- preserve process exit status;
- retain raw evidence paths;
- support mouse interaction when the selected TUI technology provides it;
- make failed assertions and violated invariants directly inspectable;
- distinguish simulated time from wall-clock time.

## Acceptance criteria

An implementation is accepted only when all of the following are demonstrated:

1. All required concepts have executable documentation and validation mappings.
2. All mandatory invariants have automated checks.
3. All hard constraints are enforceable.
4. All eight evidence commands are configured and executable.
5. The complete pipeline produces machine-readable evidence.
6. The ten-year accelerated simulation executes successfully.
7. The test system can intentionally reach controlled saturation without losing test authority or evidence integrity.
8. Recovery behavior is measured rather than assumed.
9. Autonomous optimization cannot promote a change that violates a hard invariant.
10. Every accepted evolution is reproducible from recorded evidence and configuration.
11. Every promoted change has a rollback path.
12. The same architecture can be implemented in another language by replacing `{linguagem-tal}` without changing the semantic contracts.

## Non-goals

This skill does not prescribe a framework, database, cloud provider, operating system, programming paradigm or deployment platform. Those are implementation decisions constrained by the contracts above.

It also does not claim that exhaustive testing proves the absence of all possible failures. The objective is progressively increasing behavioral coverage, discovering limits, reducing uncertainty and making evolution evidence-driven.
