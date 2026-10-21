<!-- 0x00F6 · profile README · terminal / cyberpunk / rust -->
<!-- dark & light variants are switched with <picture> + prefers-color-scheme; every asset lives in ./assets -->

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/banner.svg">
    <img src="assets/light/banner.svg" width="100%" alt="Animated terminal: cargo run --release builds and starts 0x00F6, a glitching neon 0x00F6 title appears with the tagline 'Building things that probably didn't need to be this fast.', next to a pixel-art crab and a stream of encrypted TLS and QUIC bytes being decoded into HTTP.">
  </picture>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=18&duration=2800&pause=1000&color=00F0FF&center=true&vCenter=true&width=640&height=34&lines=Hooking+the+kernel+with+eBPF+%2B+Rust+%28Aya%29;Decrypting+my+own+TLS+1.3+%2F+HTTP%2F3+traffic+%E2%80%94+live;Teaching+ClickHouse+to+read+MaxMind+DBs+%28PR+%23126009%29;Zero-copy+MMDB+decoding+in+pure+Rust;Dropping+bad+IPs+at+the+driver+with+XDP">
    <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=18&duration=2800&pause=1000&color=00728A&center=true&vCenter=true&width=640&height=34&lines=Hooking+the+kernel+with+eBPF+%2B+Rust+%28Aya%29;Decrypting+my+own+TLS+1.3+%2F+HTTP%2F3+traffic+%E2%80%94+live;Teaching+ClickHouse+to+read+MaxMind+DBs+%28PR+%23126009%29;Zero-copy+MMDB+decoding+in+pure+Rust;Dropping+bad+IPs+at+the+driver+with+XDP" alt="Typing animation cycling through: hooking the kernel with eBPF and Rust (Aya); decrypting my own TLS 1.3 and HTTP/3 traffic, live; teaching ClickHouse to read MaxMind DBs (PR #126009); zero-copy MMDB decoding in pure Rust; dropping bad IPs at the driver with XDP.">
  </picture>
</p>

<p align="center">
  <a href="PROJECTS.md"><img src="assets/badges/nav-projects.svg" height="44" alt="~/projects: detailed project sheets"></a>&nbsp;
  <a href="STACK.md"><img src="assets/badges/nav-stack.svg" height="44" alt="~/stack: languages, tools and environment"></a>&nbsp;
  <a href="WHOAMI.md"><img src="assets/badges/nav-whoami.svg" height="44" alt="~/whoami: background, interests and contact"></a>
</p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

### `~ $ whoami`

```console
$ whoami
0x00f6                      # U+00F6 → ö · 0xF6 = 246
$ cat ~/.plan
Rust-first systems & network hacker, based in Paris.
Kernel probes with eBPF, packets on the wire, keys in RAM, rows in ClickHouse.
Building things that probably didn't need to be this fast.
```

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

### `~ $ cargo tree --depth 1`

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://skillicons.dev/icons?i=rust,cpp,c,kotlin,linux,bash,git,github,cmake&theme=dark">
    <img src="https://skillicons.dev/icons?i=rust,cpp,c,kotlin,linux,bash,git,github,cmake&theme=light" alt="Skill icons: Rust, C++, C, Kotlin, Linux, Bash, Git, GitHub, CMake">
  </picture>
</p>

<p align="center">
  <img src="assets/badges/ebpf.svg" alt="eBPF">
  <img src="assets/badges/aya.svg" alt="Aya">
  <img src="assets/badges/xdp.svg" alt="XDP">
  <img src="assets/badges/tls13.svg" alt="TLS 1.3">
  <img src="assets/badges/quic-h3.svg" alt="QUIC and HTTP/3">
  <img src="assets/badges/clickhouse.svg" alt="ClickHouse">
  <img src="assets/badges/mmdb.svg" alt="MaxMind DB">
</p>

<p align="center"><sub>full manifest → <a href="STACK.md"><code>STACK.md</code></a></sub></p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

### `~ $ ls ~/projects --featured`

<p align="center">
  <a href="PROJECTS.md#0x01--ebpf-network-nexus"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/card-nexus.svg">
    <img src="assets/light/card-nexus.svg" width="49%" alt="eBPF Network Nexus card: a packet inspector where TLS, QUIC, HTTPS and DoH flows turn from encrypted bytes into readable HTTP once keys are found in memory.">
  </picture></a>
  <a href="PROJECTS.md#0x02--clickhouse--maxminddb"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/dark/card-clickhouse.svg">
    <img src="assets/light/card-clickhouse.svg" width="49%" alt="ClickHouse × MaxMindDB card: a clickhouse-client session creates a table with ENGINE = MaxMindDB('GeoLite2-City.mmdb') and looks up 8.8.8.8, which returns US.">
  </picture></a>
</p>

- **[eBPF Network Nexus](PROJECTS.md#0x01--ebpf-network-nexus)** — watches TLS, HTTPS and HTTP/3 traffic from the kernel, finds the session keys in the sending process's memory, then decrypts, decompresses and shows every flow in cleartext in a web Packet Inspector. <img src="assets/badges/source-soon.svg" height="20" alt="source: soon">
- **[ClickHouse × MaxMindDB](PROJECTS.md#0x02--clickhouse--maxminddb)** — an experimental `MaxMindDB` table engine: query a local `.mmdb` file with IPv4/IPv6 longest-prefix lookups, no import step. [![Live state of ClickHouse pull request #126009](https://img.shields.io/github/pulls/detail/state/ClickHouse/ClickHouse/126009?style=flat-square&label=PR%20%23126009&labelColor=0b1016&logo=github&logoColor=d7f9ff)](https://github.com/ClickHouse/ClickHouse/pull/126009)

<p align="center"><sub>all sheets + pinned repos → <a href="PROJECTS.md"><code>PROJECTS.md</code></a></sub></p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/divider.svg">
  <img src="assets/light/divider.svg" width="100%" alt="Section divider">
</picture>

### `~ $ git log --stat`

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api?username=0x00F6&show_icons=true&include_all_commits=true&hide_border=true&bg_color=00000000&title_color=00F0FF&text_color=C9D1D9&icon_color=FF2BD6&ring_color=FF6B2B&custom_title=%24%20git%20log%20--stat">
    <img src="https://github-readme-stats.vercel.app/api?username=0x00F6&show_icons=true&include_all_commits=true&hide_border=true&bg_color=00000000&title_color=00728A&text_color=1F2328&icon_color=C0168F&ring_color=B8430F&custom_title=%24%20git%20log%20--stat" width="56%" alt="GitHub stats for 0x00F6: stars, commits, pull requests, issues, contributions and rank.">
  </picture>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/top-langs/?username=0x00F6&layout=compact&langs_count=6&hide_border=true&bg_color=00000000&title_color=00F0FF&text_color=C9D1D9&custom_title=%24%20tokei">
    <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=0x00F6&layout=compact&langs_count=6&hide_border=true&bg_color=00000000&title_color=00728A&text_color=1F2328&custom_title=%24%20tokei" width="42%" alt="Most used languages across 0x00F6's public repositories.">
  </picture>
</p>

<details>
<summary><samp>$ cargo run --bin ferris</samp></summary>

```text
   (\/)                (\/)
    \ \    .------.    / /
     \ \  /  o  o  \  / /
      '-.(    __    ).-'
          '-.____.-'
          //  ||  \\        compiled with --release,
                            obviously.
```

</details>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&section=footer&height=110&color=0:00F0FF,50:FF2BD6,100:FF6B2B">
  <img src="https://capsule-render.vercel.app/api?type=waving&section=footer&height=110&color=0:00728A,50:C0168F,100:B8430F" width="100%" alt="Neon wave footer fading from cyan to magenta to rust orange">
</picture>

<p align="center"><samp>[process exited with code 0] · <a href="PROJECTS.md">projects</a> · <a href="STACK.md">stack</a> · <a href="WHOAMI.md">whoami</a></samp></p>
