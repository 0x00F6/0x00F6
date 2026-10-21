<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/header-stack.svg">
    <img src="assets/light/header-stack.svg" width="100%" alt="Terminal header: the command cargo tree --depth 1 is typed, then a glitching STACK title appears.">
  </picture>
</p>

<p align="center">
  <a href="README.md"><img src="assets/badges/nav-home.svg" height="40" alt="~/home: back to the profile README"></a>&nbsp;
  <a href="PROJECTS.md"><img src="assets/badges/nav-projects.svg" height="40" alt="~/projects: detailed project sheets"></a>&nbsp;
  <a href="WHOAMI.md"><img src="assets/badges/nav-whoami.svg" height="40" alt="~/whoami: background, interests and contact"></a>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/neofetch.svg">
    <img src="assets/light/neofetch.svg" width="100%" alt="neofetch-style summary next to a pixel-art crab. OS: Linux with eBPF. Langs: Rust, C++, C, Kotlin, SQL. Kernel: eBPF, Aya, XDP. Net: TLS 1.3, QUIC, HTTP/3, HTTP/2. Data: ClickHouse, MaxMind DB. Edge: HAProxy SPOA, FireHOL. Build: cargo, CMake. Motto: didn't need to be this fast.">
  </picture>
</p>

```toml
# ~/Cargo.toml: what 0x00F6 is built from
[package]
name    = "0x00f6"
version = "0.0.246"             # 0xF6
edition = "2024"

[dependencies]
rust       = { version = "stable", features = ["aya", "zero-copy", "release-profile"] }
ebpf       = { features = ["xdp", "kernel-capture", "maps"] }
networking = { features = ["tls13", "quic", "http3", "http2", "haproxy-spoa"] }
clickhouse = { features = ["table-engines", "cpp"] }
maxminddb  = { features = ["mmdb-v2", "ipv4", "ipv6"] }

[target.'cfg(target_os = "linux")'.dependencies]
linux = "*"

[profile.release]
opt-level = 3                   # it probably didn't need to be this fast
```

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

## `[languages]`

| | where it runs |
| --- | --- |
| <img src="assets/badges/rust.svg" alt="Rust"> | **first choice.** eBPF tooling with Aya, network agents, MMDB parsing, everything new |
| <img src="assets/badges/cpp.svg" alt="C++"> | ClickHouse internals: the `MaxMindDB` table engine |
| <img src="assets/badges/c.svg" alt="C"> | `libmaxminddb`, bundled and wired into ClickHouse |
| <img src="assets/badges/sql.svg" alt="SQL"> | ClickHouse queries and functional tests |
| <img src="assets/badges/kotlin.svg" alt="Kotlin"> | Android: [blink-sentinel](https://github.com/0x00F6/blink-sentinel) |

## `[kernel]`

<p>
  <img src="assets/badges/ebpf.svg" alt="eBPF">
  <img src="assets/badges/aya.svg" alt="Aya">
  <img src="assets/badges/xdp.svg" alt="XDP">
  <img src="assets/badges/linux.svg" alt="Linux">
</p>

- **eBPF** — XDP programs at the driver level, kernel-side traffic capture, maps to hand data to userspace
- **Aya** — eBPF written in Rust on both sides of the boundary
- **Linux** — sockets, the network stack, and process memory when keys are hiding there

## `[network]`

<p>
  <img src="assets/badges/tls13.svg" alt="TLS 1.3">
  <img src="assets/badges/quic-h3.svg" alt="QUIC and HTTP/3">
  <img src="assets/badges/http2.svg" alt="HTTP/2">
  <img src="assets/badges/haproxy.svg" alt="HAProxy SPOA">
  <img src="assets/badges/firehol.svg" alt="FireHOL">
</p>

- **crypto & transport** — TLS 1.2 / 1.3 record layer, QUIC
- **application** — HTTP/1.1, HTTP/2, HTTP/3
- **edge** — HAProxy SPOA agents, FireHOL IP reputation lists
- **IP intelligence** — MaxMind DB v2, IPv4/IPv6 longest-prefix lookups

## `[data]`

<p>
  <img src="assets/badges/clickhouse.svg" alt="ClickHouse">
  <img src="assets/badges/mmdb.svg" alt="MaxMind DB">
</p>

- **ClickHouse** — table engines, IPv4/IPv6 types, functional tests ([PR #126009](https://github.com/ClickHouse/ClickHouse/pull/126009))
- **MaxMind DB** — the `.mmdb` format from the inside: reading *and* writing it ([libmaxminddb-rs](https://github.com/0x00F6/libmaxminddb-rs))

## `[tooling]`

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://skillicons.dev/icons?i=rust,cpp,c,kotlin,linux,bash,git,github,cmake&theme=dark">
    <img src="https://skillicons.dev/icons?i=rust,cpp,c,kotlin,linux,bash,git,github,cmake&theme=light" alt="Skill icons: Rust, C++, C, Kotlin, Linux, Bash, Git, GitHub, CMake">
  </picture>
</p>

- **build** — cargo, CMake
- **ship** — git, GitHub, GitHub Pages for docs ([libmaxminddb-rs](https://0x00f6.github.io/libmaxminddb-rs))
<!-- ✏️ editor · terminal · shell · distro — add your daily drivers here, e.g. "- **desk** — neovim · alacritty · zsh · Arch" -->

<p align="center">
  <a href="README.md"><img src="assets/badges/nav-home.svg" height="40" alt="~/home: back to the profile README"></a>&nbsp;
  <a href="PROJECTS.md"><img src="assets/badges/nav-projects.svg" height="40" alt="~/projects: detailed project sheets"></a>&nbsp;
  <a href="WHOAMI.md"><img src="assets/badges/nav-whoami.svg" height="40" alt="~/whoami: background, interests and contact"></a>
</p>
