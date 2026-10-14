<!-- Generated from site/data/libraries.yaml in ubgo.github.io by `task profile`. Edit the data file there, not this file. -->

<p align="center"><img src="ubgo-icon-512.png" alt="ubgo logo: a bold lowercase u holding one amber block" width="72" height="72"></p>
<h1 align="center">ubgo</h1>
<p align="center"><strong>Batteries included for Go, one module at a time.</strong></p>
<p align="center"><em>Early alpha: ubgo is still being built and is not fully production-ready yet, so libraries and APIs may change.</em></p>
<p align="center">Open-source Go libraries, plus a few TypeScript ones, for authentication, errors, logging, caching, config, SQL, GraphQL, HTTP services, crypto and tooling.</p>
<p align="center">
  <a href="https://ubgo.github.io"><img src="https://img.shields.io/badge/site-ubgo.github.io-0891B2" alt="Website: ubgo.github.io"></a>
  <img src="https://img.shields.io/badge/public%20libraries-46-0891B2" alt="46 public libraries">
  <img src="https://img.shields.io/badge/language-Go%20%C2%B7%20TypeScript-0891B2" alt="Languages: Go and TypeScript">
  <img src="https://img.shields.io/badge/license-Apache--2.0-0891B2" alt="License: Apache-2.0">
</p>

ubgo is an ecosystem for building Go apps, in the spirit of the components Laravel ships for authentication, caching, logging and configuration. Every piece is its own Go module, so a service imports only what it uses: sign-in, sessions, two-factor, passkeys, OAuth and organizations, structured errors and logging, caching with Redis, Postgres, Memcached and in-memory backends, typed configuration and .env files, SQL building, GraphQL and ent helpers, health checks, graceful shutdown and crypto. The main libraries share one shape, a small core with adapters outside it and a shared test suite, so learning one teaches you the next.

- [Libraries by area](#libraries-by-area)
- [Volt](#volt)
- [Upcoming](#upcoming)
- [Principles](#principles)
- [Install](#install)
- [FAQ](#faq)

## Libraries by area

### Auth and identity

- [**auth**](https://github.com/ubgo/auth): Embeddable authentication with plugins for email, password, phone, OAuth, passkeys, 2FA, API keys, JWT and organizations, stored in your own Postgres, MySQL or SQLite.

### Errors and logging

- [**errx**](https://github.com/ubgo/errx): One structured error type with stable identity, class, redactable fields, return traces and a wire codec.
- [**goerr**](https://github.com/ubgo/goerr): Error type with separate operator and user messages, error codes, key/value data and trace IDs.
- [**logger**](https://github.com/ubgo/logger): Adapter-based, slog-native structured logging with sampling, redaction, OpenTelemetry and rotation.
- [**otelkit**](https://github.com/ubgo/otelkit): One constructor that sets up OpenTelemetry traces, metrics and logs, with presets for common backends.

### Caching

- [**cache**](https://github.com/ubgo/cache): The core cache interface with generics, single-flight Remember, a distributed locker and a shared conformance suite.
- [**cache-cli**](https://github.com/ubgo/cache-cli): Command-line cache inspector (get, set, del, stats, keys) with JSON output, built on cache. *(CLI)*
- [**cache-cluster**](https://github.com/ubgo/cache-cluster): Peer-aware distributed cache with a consistent-hash ring and HTTP peer fill, on any cache backend.
- [**cache-examples**](https://github.com/ubgo/cache-examples): Runnable examples for the cache family, one self-contained program per feature. *(examples)*
- [**cache-mem**](https://github.com/ubgo/cache-mem): Sharded in-memory backend for cache with W-TinyLFU or LRU eviction and optional snapshots.
- [**cache-memcached**](https://github.com/ubgo/cache-memcached): Memcached backend for cache, covering the parts of the interface Memcached supports.
- [**cache-obj**](https://github.com/ubgo/cache-obj): In-process cache that holds live Go objects by reference, with TTL and LRU and no serialization.
- [**cache-pg**](https://github.com/ubgo/cache-pg): Postgres and SQLite backend for cache over database/sql, with Migrate and Vacuum.
- [**cache-redis**](https://github.com/ubgo/cache-redis): Redis 6+ backend for cache with prefix isolation and Pub/Sub invalidation across processes.
- [**cache-tiered**](https://github.com/ubgo/cache-tiered): Stacks cache backends into L1/L2/L3 tiers with read promotion and per-tier TTL.
- [**threadsafecache**](https://github.com/ubgo/threadsafecache): Generic thread-safe LRU and TTL cache. Deprecated; use cache-obj instead.

### Config and env

- [**cfgkit**](https://github.com/ubgo/cfgkit): Typed config from env, .env, JSON, YAML, TOML, flags and secret stores into one validated struct.
- [**dotenv**](https://github.com/ubgo/dotenv): .env parser and editor that keeps comments, order and quoting, plus the dotenvctl CLI.

### SQL and data

- [**gormuuid**](https://github.com/ubgo/gormuuid): Postgres uuid[] field type for GORM.
- [**gouuid**](https://github.com/ubgo/gouuid): Small helpers around google/uuid.
- [**jsonslice**](https://github.com/ubgo/jsonslice): A JSON-backed slice that round-trips through SQL columns and gqlgen scalars.
- [**jsontype**](https://github.com/ubgo/jsontype): A JSON type that round-trips between Go, JSON and SQL drivers (Postgres jsonb, MySQL json, SQLite).
- [**lock**](https://github.com/ubgo/lock): One lock interface with five backends (filelock, flock, Redis, Postgres, etcd) and fencing tokens.
- [**publicid**](https://github.com/ubgo/publicid): URL-safe, non-sequential public IDs from a fixed lowercase nanoid alphabet.
- [**sqlb**](https://github.com/ubgo/sqlb): Typed SQL builder with compile-checked columns and joins, Postgres and ClickHouse packages and a driver conformance suite.

### GraphQL and ent

- [**entkit**](https://github.com/ubgo/entkit): Column types and field helpers for ent and gqlgen, as small independent modules.
- [**entx**](https://github.com/ubgo/entx): Extensions for ent such as polymorphic relations, cascade delete and per-API GraphQL schemas.
- [**gqlgenfn**](https://github.com/ubgo/gqlgenfn): Helper functions for using gqlgen with Gin.
- [**gqlkit**](https://github.com/ubgo/gqlkit): Generates typed GraphQL client SDKs for Go and TypeScript with compile-checked field selection.
- [**gqlmodel**](https://github.com/ubgo/gqlmodel): Custom scalar field types for gqlgen.
- [**gqlutil**](https://github.com/ubgo/gqlutil): Small helper functions for gqlgen.

### HTTP and services

- [**buildinfo**](https://github.com/ubgo/buildinfo): Version, commit, build time and module info for Go binaries, from runtime/debug with -ldflags overrides.
- [**buildinfo-examples**](https://github.com/ubgo/buildinfo-examples): Runnable example apps for buildinfo, from ldflags stamping to HTTP, OpenTelemetry, Zap and slog. *(examples)*
- [**gofm**](https://github.com/ubgo/gofm): An early framework for building Go microservices.
- [**health**](https://github.com/ubgo/health): Thread-safe health and readiness registry with k8s-style probes, framework adapters and ready-made checkers.
- [**health-examples**](https://github.com/ubgo/health-examples): Runnable example apps for health, covering every HTTP framework adapter and observability. *(examples)*
- [**httpreq**](https://github.com/ubgo/httpreq): JSON-over-HTTP calls on top of net/http with one function, options and typed errors.
- [**shutdown**](https://github.com/ubgo/shutdown): Phased graceful shutdown for services, parallel within a phase, with a watchdog and telemetry hooks.
- [**shutdown-examples**](https://github.com/ubgo/shutdown-examples): Runnable examples for shutdown. *(examples)*

### Crypto

- [**crypt**](https://github.com/ubgo/crypt): Go crypto with safe defaults (AES-GCM, ChaCha20-Poly1305, argon2id, HMAC, Ed25519, key rotation), byte-compatible with crypt-ts.
- [**crypt-ts**](https://github.com/ubgo/crypt-ts): TypeScript and Node.js crypto with safe defaults over node:crypto, byte-compatible with the Go crypt.

### Tooling

- [**docsync**](https://github.com/ubgo/docsync): Finds the sentences in your docs that stopped being true when the code they describe changed.
- [**gots**](https://github.com/ubgo/gots): Generates TypeScript types, enums, constants and interfaces from Go source. *(CLI)*
- [**goutil**](https://github.com/ubgo/goutil): A small set of everyday Go helper functions.
- [**lath**](https://github.com/ubgo/lath): A task runner where tasks are typed Go functions and a deploy runs the same on a laptop, over ssh and in CI. *(CLI)*
- [**ubgo-skills**](https://github.com/ubgo/ubgo-skills): Reusable skill files that capture Go and frontend coding conventions.

## Volt

Volt is the layer on top of ubgo to build, release and ship Go CLIs and libraries: the `volt` tool (scaffold, CI gate, coverage, cross-platform builds, verified releases) plus importable kit modules for building the CLIs themselves.

```sh
brew install khanakia/tap/volt
```

- [**voltkit**](https://github.com/ubgo/voltkit): The Volt tool to scaffold, check, build, release and ship Go CLIs and libraries in any repo layout, plus importable kit modules for building the CLIs themselves.
- [**volt-cli**](https://github.com/ubgo/volt-cli): Templates for volt new cli, a stdlib-only minimal CLI and a cobra variant, fetched at a pinned tag.
- [**volt-action**](https://github.com/ubgo/volt-action): GitHub Action that installs the released Volt binary, checksum-verified, and runs one command such as volt ci or volt release.
- [**volt-demo-cli**](https://github.com/ubgo/volt-demo-cli): Demo of a single-CLI repo released with Volt, with install scripts, workflows and a skills command generated by volt gen.
- [**volt-demo-clis**](https://github.com/ubgo/volt-demo-clis): Demo of a monorepo with two CLIs, nested libraries and an internal module, each released on its own tag stream.
- [**volt-demo-lib**](https://github.com/ubgo/volt-demo-lib): Demo of a single-library repo, released with notes and a verified module proxy entry instead of binaries.

## Upcoming

These exist but are not public yet, so they have no links. More libraries are on the way.

- **workflow**: Embeddable Go library for cron schedules, delayed and background jobs with retries, and multi-step workflows behind one Client interface, with swappable drivers (in-memory, SQL and Hatchet).
- **brick**: A component-based HTML render engine for Go built on html/template, with layouts, components, islands and server actions, and a 133-component UI kit.
- **validator**: Struct-native Go validator with a serializable IR; one set of rules validates in Go, exports to JSON Schema, and runs as a Standard-Schema TypeScript validator.
- **volt-api**: The batteries-included Go backend starter, with schema-first GraphQL (gqlgen), Ent ORM, NATS JetStream, type-safe PKL config, OpenTelemetry, CLI and cron.
- **volt-web**: A production-ready TanStack Start boilerplate for SSR React apps, with a dashboard shell, tRPC and oRPC, typed GraphQL via gqlkit, Drizzle and PostgreSQL.

## Principles

These hold for the libraries named under each point, as their own READMEs state. They are not a promise for every repo.

- **Small cores.** The core module has no third-party dependencies, so importing it adds nothing to your go.sum. For example: [errx](https://github.com/ubgo/errx), [logger](https://github.com/ubgo/logger), [health](https://github.com/ubgo/health), [shutdown](https://github.com/ubgo/shutdown), [buildinfo](https://github.com/ubgo/buildinfo), [sqlb](https://github.com/ubgo/sqlb), [lock](https://github.com/ubgo/lock), [httpreq](https://github.com/ubgo/httpreq).
- **Adapters live outside the core.** Integrations (frameworks, OpenTelemetry, drivers, secret stores) ship as separate modules, so you only download what you import. For example: [errx](https://github.com/ubgo/errx), [logger](https://github.com/ubgo/logger), [health](https://github.com/ubgo/health), [shutdown](https://github.com/ubgo/shutdown), [buildinfo](https://github.com/ubgo/buildinfo), [cfgkit](https://github.com/ubgo/cfgkit), [sqlb](https://github.com/ubgo/sqlb), [otelkit](https://github.com/ubgo/otelkit), [lock](https://github.com/ubgo/lock), [auth](https://github.com/ubgo/auth).
- **Shared conformance suites.** A family's contract is a test suite that every backend runs, so backends behave the same. For example: [cache](https://github.com/ubgo/cache), [cache-obj](https://github.com/ubgo/cache-obj), [sqlb](https://github.com/ubgo/sqlb).

## Install

Most libraries install with:

```sh
go get github.com/ubgo/<name>
```

[auth](https://github.com/ubgo/auth) is not tagged yet; install the newest commit with `go get github.com/ubgo/auth@latest`.

Some are split into sub-modules or ship a CLI to `go install`. Each repo's README, and its page on [ubgo.github.io](https://ubgo.github.io/libraries/), gives the exact line.

## FAQ

**Do I need to install everything?** No. Every library is its own Go module (and some split further into sub-modules), so you add only the ones you use.

**Where are the docs?** Each repository's README, plus its page on pkg.go.dev (or npm for the TypeScript ones). The [library index](https://ubgo.github.io/libraries/) links to both.

**What license are they under?** Every library is open source under Apache-2.0. The LICENSE file in each repository is the source of truth.

**Where do I report a bug?** Open an issue in that library's repository.
