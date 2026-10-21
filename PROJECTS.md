<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/header-projects.svg">
    <img src="assets/light/header-projects.svg" width="100%" alt="Terminal header: the command cat PROJECTS.md is typed, then a glitching PROJECTS title appears.">
  </picture>
</p>

<p align="center">
  <a href="README.md"><img src="assets/badges/nav-home.svg" height="40" alt="~/home: back to the profile README"></a>&nbsp;
  <a href="STACK.md"><img src="assets/badges/nav-stack.svg" height="40" alt="~/stack: languages, tools and environment"></a>&nbsp;
  <a href="WHOAMI.md"><img src="assets/badges/nav-whoami.svg" height="40" alt="~/whoami: background, interests and contact"></a>
</p>

```console
$ ls -l ~/projects
drwxr-xr-x  0x00f6  ebpf-network-nexus/   TLS · HTTPS · HTTP/3, keys straight from RAM
drwxr-xr-x  0x00f6  clickhouse/           MaxMindDB table engine · PR #126009 (1/3)
drwxr-xr-x  0x00f6  pinned/               4 more repos, listed at the bottom
```

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

## 0x01 — eBPF Network Nexus

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/card-nexus.svg">
    <img src="assets/light/card-nexus.svg" width="62%" alt="eBPF Network Nexus packet inspector: TLS, QUIC, HTTPS and DoH flows start as encrypted bytes, a scan sweeps the table once keys are found in memory, and each payload turns into readable HTTP.">
  </picture>
</p>

<p align="center">
  <img src="assets/badges/rust.svg" alt="Rust">
  <img src="assets/badges/ebpf.svg" alt="eBPF">
  <img src="assets/badges/linux.svg" alt="Linux">
  <img src="assets/badges/tls13.svg" alt="TLS 1.3">
  <img src="assets/badges/quic-h3.svg" alt="QUIC and HTTP/3">
  <img src="assets/badges/http2.svg" alt="HTTP/2">
  <img src="assets/badges/source-soon.svg" alt="Source: soon">
</p>

### `▸ problem`

Almost everything on the wire is encrypted now: TLS 1.3, HTTPS, HTTP/3 over QUIC. Great for privacy, painful when you need to see what **your own** processes are actually saying. Proxies have to sit in the middle and change the traffic; key-log files only work when the application cooperates.

### `▸ approach`

1. **Observe** — eBPF programs capture TLS records and QUIC datagrams in the kernel and tie each flow to the process that sent it.
2. **Hunt** — the agent scans that process's memory for candidate AES (and other) session keys.
3. **Decrypt** — candidates are tested against the captured records; the one that decrypts them unlocks the flow.
4. **Decompress & parse** — bodies are inflated, then HTTP/1.1, HTTP/2 and HTTP/3 are rebuilt into readable exchanges.
5. **Inspect** — everything streams to a web **Packet Inspector** with a *perspective* table, served on `localhost:8080`.

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/nexus-pipeline.svg">
    <img src="assets/light/nexus-pipeline.svg" width="100%" alt="Architecture: in the kernel, eBPF programs capture TLS records and QUIC datagrams and send events to userspace. The Rust agent scans the target process memory for key candidates, verifies them, decrypts, decompresses and parses HTTP/1.1, HTTP/2 and HTTP/3, then streams cleartext flows to the web Packet Inspector on port 8080.">
  </picture>
</p>

> [!WARNING]
> Nexus reads other processes' memory and decrypts their traffic. Run it only on machines you own or are explicitly authorized to analyze.

### `▸ tech`

| layer | stack |
| --- | --- |
| kernel | eBPF programs on Linux |
| agent | Rust, userspace |
| crypto | TLS record layer · QUIC packet protection · AES session keys |
| protocols | HTTP/1.1 · HTTP/2 · HTTP/3 |
| ui | web Packet Inspector · `localhost:8080` |

### `▸ links`

- **source** — not public yet, coming soon <!-- ✏️ add the repository URL here once it is public -->
- **related** — [eBPF-ip-reputation-firewall](https://github.com/0x00F6/eBPF-ip-reputation-firewall): the same kernel-side toolbox (Rust + Aya + XDP), pointed at dropping bad IPs instead of reading good ones

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

## 0x02 — ClickHouse × MaxMindDB

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/card-clickhouse.svg">
    <img src="assets/light/card-clickhouse.svg" width="62%" alt="A clickhouse-client session: enable allow_experimental_maxminddb_table_engine, create table geoip with ENGINE = MaxMindDB('GeoLite2-City.mmdb') and refresh_interval 5m, then select country.iso_code for ip 8.8.8.8, which returns US.">
  </picture>
</p>

<p align="center">
  <img src="assets/badges/cpp.svg" alt="C++">
  <img src="assets/badges/clickhouse.svg" alt="ClickHouse">
  <img src="assets/badges/mmdb.svg" alt="MaxMind DB">
  <img src="assets/badges/cmake.svg" alt="CMake">
  <img src="assets/badges/sql.svg" alt="SQL">
  <img src="assets/badges/engine-experimental.svg" alt="Engine: experimental">
  <img src="assets/badges/split-1-of-3.svg" alt="Series: part 1 of 3">
  <a href="https://github.com/ClickHouse/ClickHouse/pull/126009"><img src="https://img.shields.io/github/pulls/detail/state/ClickHouse/ClickHouse/126009?style=flat-square&label=PR%20%23126009&labelColor=0b1016&logo=github&logoColor=d7f9ff" height="28" alt="Live state of ClickHouse pull request #126009"></a>
</p>

### `▸ problem`

Enriching access logs with GeoIP data in ClickHouse usually means importing MaxMind data first, then keeping that copy in sync with every database release. But the `.mmdb` file is already a compact binary search tree built for exactly these lookups, so why not query it in place?

### `▸ approach`

An experimental, read-only `MaxMindDB` table engine that answers lookups straight from the file:

- **opt-in** — gated by `allow_experimental_maxminddb_table_engine`; built on a bundled `libmaxminddb` 1.14.1, wired in as an optional CMake dependency.
- **local & safe** — `.mmdb` files are read only from the server's `user_files_path`, with `READ ON FILE` enforced.
- **fast path** — IPv4 and IPv6 longest-prefix lookups driven by bounded `WHERE ip = …` / `WHERE ip IN (…)` predicates.
- **typed** — manual schemas or automatic inference, nested tuples / arrays / maps, and only the requested fields get decoded.
- **hot swaps** — replacement files are validated against the persisted schema, and running readers keep their own immutable generation.

```sql
SET allow_experimental_maxminddb_table_engine = 1;

CREATE TABLE geoip ENGINE = MaxMindDB('GeoLite2-City.mmdb')
SETTINGS refresh_interval = '5m';

SELECT country.iso_code FROM geoip WHERE ip = toIPv4('8.8.8.8');
```

<details>
<summary><samp>$ git log --oneline --graph maxminddb</samp> · how the work is split</summary>
<br>

The original [#123672](https://github.com/ClickHouse/ClickHouse/pull/123672) was split into three reviewable, stacked changes, as asked during review.

| step | scope | where |
| --- | --- | --- |
| **1/3 core** | local engine, schema inference, IPv4/IPv6 lookups, functional tests, docs | [ClickHouse#126009](https://github.com/ClickHouse/ClickHouse/pull/126009) |
| **2/3 advanced** | direct `JOIN`, snapshots, bounded decoding caches | [0x00F6/ClickHouse#1](https://github.com/0x00F6/ClickHouse/pull/1) |
| **3/3 remote** | HTTP / S3 sources, authentication, security, hot reload | [0x00F6/ClickHouse#2](https://github.com/0x00F6/ClickHouse/pull/2) |

Steps 2 and 3 live on the fork until their base branches exist upstream.

</details>

### `▸ tech`

| layer | stack |
| --- | --- |
| engine | C++ inside the ClickHouse server |
| reader | `libmaxminddb` (C), bundled |
| build | CMake, optional dependency |
| query | SQL · IPv4 / IPv6 types |
| data | MaxMind DB (`.mmdb`) |

### `▸ links`

- **pull request** — [ClickHouse/ClickHouse#126009](https://github.com/ClickHouse/ClickHouse/pull/126009) (part 1 of 3, live state in the badge above)
- **origin** — [ClickHouse/ClickHouse#123672](https://github.com/ClickHouse/ClickHouse/pull/123672)
- **related** — [libmaxminddb-rs](https://github.com/0x00F6/libmaxminddb-rs): a pure Rust MMDB v2 reader *and* writer with zero-copy decoding · [docs](https://0x00f6.github.io/libmaxminddb-rs)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

## `$ ls ~/projects/pinned`

| repo | what it does | lang |
| --- | --- | --- |
| [libmaxminddb-rs](https://github.com/0x00F6/libmaxminddb-rs) | Pure Rust MaxMind DB v2 (IPv4/IPv6) reader and writer, zero-copy borrowed decoding · [docs](https://0x00f6.github.io/libmaxminddb-rs) | <img src="assets/badges/rust.svg" alt="Rust"> |
| [eBPF-ip-reputation-firewall](https://github.com/0x00F6/eBPF-ip-reputation-firewall) | Ultra-low-latency ingress firewall in Rust with Aya, filtering at the NIC driver level with XDP | <img src="assets/badges/rust.svg" alt="Rust"> |
| [haproxy-spoa-ip-reputation-firehol](https://github.com/0x00F6/haproxy-spoa-ip-reputation-firehol) | HAProxy external agent (SPOA) that blocks malicious IPs in real time from FireHOL blocklists | <img src="assets/badges/rust.svg" alt="Rust"> |
| [blink-sentinel](https://github.com/0x00F6/blink-sentinel) | Arms and disarms a Blink system from your phone's Wi-Fi or Bluetooth presence | <img src="assets/badges/kotlin.svg" alt="Kotlin"> |

<p align="center">
  <a href="README.md"><img src="assets/badges/nav-home.svg" height="40" alt="~/home: back to the profile README"></a>&nbsp;
  <a href="STACK.md"><img src="assets/badges/nav-stack.svg" height="40" alt="~/stack: languages, tools and environment"></a>&nbsp;
  <a href="WHOAMI.md"><img src="assets/badges/nav-whoami.svg" height="40" alt="~/whoami: background, interests and contact"></a>
</p>
