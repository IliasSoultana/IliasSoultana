## Ilias Amir Soultana

Computer Science student at TU Dortmund, working on software security at the
binary and compiler level.

Most of what I build asks one question in different forms: **what does a
compiled artefact actually guarantee?** Not what the source intended, not what
the build flags claimed - what survived into the binary that ships. That gap
is where exploitation lives, and it is invisible unless something goes looking
for it.

---

### Binary & compiler security

**[hardening-check](https://github.com/IliasSoultana/hardening-check)** · Python
Parses ELF headers and reports which exploit mitigations a binary was really
compiled with - PIE, NX, stack canary, RELRO. JSON output and a `--fail-under`
gate, so a dropped build flag stops a pipeline instead of shipping silently.

**[llvm-hardeningpass](https://github.com/IliasSoultana/llvm-hardeningpass)** · C++
The same question one stage earlier: an LLVM module pass that reads SSP,
SafeStack and ShadowCallStack attributes per function at IR level, before the
linker exists. Catches what the ELF scanner cannot — a binary can carry canary
machinery while individual functions go uninstrumented.

**[diversity-poc](https://github.com/IliasSoultana/diversity-poc)** · Python, Clang
`divcc`, a compiler wrapper that derives a per-device seed and shuffles link
order, so the same source yields functionally identical but structurally
different binaries. An exploit written against fixed addresses on one unit
does not transfer to the next. Coarse by construction — it moves whole
objects, not instructions — and the README says exactly where that stops
helping.

**[elfharden](https://github.com/IliasSoultana/elfharden)** · Go ·
**[elfharden-rs](https://github.com/IliasSoultana/elfharden-rs)** · Rust
The ELF scanner reimplemented twice more, against `debug/elf` and `goblin`.
Cross-checked on the same corpus: three parsers, three languages, one set of
answers. Disagreement between them is a bug in one of them, which is the point.

### Infrastructure

**[telemetry-stack](https://github.com/IliasSoultana/telemetry-stack)** · Helm, k3s
MQTT broker, exporter, Prometheus and Grafana as a single chart, deployed to
k3s with `kubeconform` validation in CI.

---

### Elsewhere

Embedded work from an internship at Fraunhofer IMS: ESP32-S3 firmware under
FreeRTOS and its OTA update path, where updates were authenticated by a plain
SHA-256 checksum - proof a file arrived intact, but not proof of who sent it.
Anyone reaching the MQTT broker could publish firmware to the fleet. Closed
with an HMAC-SHA256 signature the device verifies before download.

Currently reading toward exploitation and agent security - the two directions
where "what does this actually guarantee" gets most interesting.

📍 Hagen, Germany · 📧 smilsou1@unimail.tu-dortmund.de
