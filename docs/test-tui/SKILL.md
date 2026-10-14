# SKILL — Official Evidence TUI Executor

## Role

This skill defines the official terminal user interface for executing and observing the architecture evidence suite defined by the root `SKILL.md`.

The reference implementation technology is **Ratatui on Rust**, with a terminal event/input backend capable of mouse events. Ratatui is selected because it provides a broad widget model, composable layouts, tables, lists, gauges, charts, sparklines, logs, scrolling regions and interactive terminal rendering while remaining suitable for a continuously updating test dashboard.

The TUI is an executor and observer. It MUST NOT become the semantic authority for architecture rules. `config.yml`, test contracts and machine-readable evidence remain authoritative.

## Language rule

<!-- IMPORTANT: Replace every occurrence of "{linguagem-tal}" with the target implementation language before using this skill. -->

The TUI implementation MAY use a different language from the system under test. The only required integration contract is the configured evidence command interface and structured evidence protocol.

## Required commands

The TUI MUST expose exactly these official logical actions:

- `run:unitary:evidence`
- `run:bdd:evidence`
- `run:load:evidence`
- `run:stress:evidence`
- `run:chaos:evidence`
- `run:security:evidence`
- `run:benchmark:evidence`
- `run:pipeline:evidence`

The commands themselves are read from `config.yml`. The TUI MUST NOT hard-code the implementation command behind a logical name.

## Execution model

For each command, the executor MUST:

1. Resolve the logical command from `config.yml`.
2. Start the process without altering its configured semantics.
3. Capture stdout and stderr without blocking the UI loop.
4. Parse structured evidence events when available.
5. Preserve raw process output.
6. Display live status and metrics.
7. Record start/end wall-clock time.
8. Record simulated time when the test exposes it.
9. Capture exit status.
10. Mark the command PASS, FAIL, CANCELLED or BLOCKED.
11. Preserve evidence even when the process fails.

The TUI MUST support sequential pipeline execution and SHOULD support independent evidence stages concurrently when `config.yml` explicitly permits concurrency.

## Ten-year simulation

The TUI MUST understand the official accelerated simulation contract:

`10 wall-clock seconds = 1 simulated day`

A complete ten-year horizon therefore represents 3650 simulated days. The dashboard MUST show both:

- wall-clock elapsed time;
- simulated date/day;
- simulation acceleration ratio;
- current scenario.

The TUI MUST NOT confuse simulated time with actual elapsed time.

## Dashboard

The default screen SHOULD contain the maximum useful information without making the terminal unreadable. The recommended layout contains:

- global pipeline status;
- current command;
- command queue;
- simulated date and day;
- wall-clock elapsed time;
- overall progress;
- pass/fail/cancelled counters;
- requests per second;
- total requests;
- successful requests;
- failed requests;
- error rate;
- p50 latency;
- p95 latency;
- p99 latency;
- throughput;
- CPU utilization;
- memory utilization;
- active concurrency;
- queue depth;
- saturation state;
- discovered limit;
- current operating envelope;
- chaos experiment status;
- security finding count;
- benchmark delta versus baseline;
- invariant violations;
- latest evidence event;
- scrollable live log;
- evidence artifact path.

## Interaction

Mouse interaction SHOULD be enabled. When supported by the terminal backend, the following interactions SHOULD exist:

- click a test stage to open its detailed evidence;
- click a failure to inspect the assertion and context;
- click a metric to expand its time series;
- click a scenario to inspect its generated inputs;
- click an invariant violation to inspect the violated contract;
- click a command to start or cancel it when allowed;
- scroll logs and tables;
- select a historical evidence record;
- switch between dashboard, tests, metrics, failures, chaos, security and evidence views.

Keyboard equivalents MUST exist for every safety-relevant mouse action.

## Evidence event protocol

The preferred event shape is language-independent structured data. A conceptual event MUST be able to represent:

- event type;
- test name;
- command name;
- scenario identifier;
- simulated timestamp;
- wall-clock timestamp;
- status;
- assertion;
- measured values;
- resource values;
- error information;
- invariant identifier;
- artifact reference.

The TUI MUST tolerate unstructured output, but unstructured output MUST NOT be mistaken for complete structured evidence.

## Safety requirements

The TUI MUST NOT:

- silently retry destructive experiments;
- remove or alter evidence after a failure;
- hide invariant violations;
- reinterpret a non-zero process exit as success;
- allow cancellation to corrupt the evidence record;
- bypass configured experiment limits;
- execute commands not present in the configured command registry unless an explicit operator action permits it.

A cancellation request MUST propagate to the running test and MUST result in an auditable CANCELLED state.

## Test views

### Overview

Shows the current pipeline, overall health, simulation progress and primary metrics.

### Evidence

Shows individual assertions, scenario results, invariants, constraints and artifact references.

### Metrics

Shows live and historical measurements with selectable time windows.

### Failures

Shows failures grouped by test, scenario, invariant and suspected cause.

### Chaos

Shows active fault injection, blast radius, recovery state and experiment result.

### Security

Shows security test status, findings, severity and affected contract without exposing secrets.

### Benchmarks

Shows baseline, current measurement, delta and acceptance result.

### Logs

Shows timestamped process output and structured events with filtering and scrolling.

## Acceptance criteria

The TUI is accepted only if:

1. Every official evidence command can be configured without changing TUI code.
2. Every command has a visible live state.
3. Process exit codes are preserved correctly.
4. Stdout/stderr remain observable during execution.
5. Structured evidence is displayed without losing raw evidence.
6. The ten-year accelerated simulation is visible and correctly represented.
7. Mouse interaction works when the terminal supports it.
8. Keyboard-only operation remains possible.
9. Cancellation is safe and auditable.
10. Failures and invariant violations cannot be hidden by UI state.
11. The TUI remains responsive while tests produce high-rate output.
12. The TUI can execute the complete pipeline through `run:pipeline:evidence`.
13. Evidence artifacts remain accessible after process termination.
14. The TUI itself does not become a hidden architectural dependency of the system under test.

## Performance acceptance

The TUI MUST remain responsive while receiving high-rate test output. Rendering frequency MAY be throttled independently of event ingestion. The executor MUST avoid coupling process throughput to terminal rendering throughput.

For high-volume load tests, metrics SHOULD be aggregated incrementally rather than rendering every request as a UI event.

## Architecture boundary

The executor has four conceptual layers:

`Command Registry → Process Supervisor → Evidence Stream → TUI Renderer`

The process supervisor owns lifecycle and cancellation. The evidence stream owns normalized observations. The renderer owns presentation. None of these layers may redefine architecture acceptance criteria.
