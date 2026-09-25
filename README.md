## Ilias Amir Soultana

Computer Science student at TU Dortmund. I work on software security at the level
where the abstractions run out: the compiled binary, and the instructions a CPU
actually executes.

What keeps me there is a gap I find hard to look away from. Source code says what
a program is meant to do. Build flags say how it is meant to be protected. The
only thing that ships is the binary, and it does not always agree with either.
Most of what I build is a different way of asking the same question, what a
compiled artefact actually became, and lately what I can change about it after
the fact, with no source and no rebuild.

I am early. Third semester, more curiosity than track record. I have decided to
treat that as a reason to go deeper than my courses ask rather than a reason to
wait, because the things worth being good at here take years, and the sooner you
start the more they compound.

---

### Binary and compiler security

**[hardening-check](https://github.com/IliasSoultana/hardening-check)** · Python
Parses ELF headers and reports which exploit mitigations a binary was really
compiled with: PIE, NX, stack canary, RELRO. JSON output and a `--fail-under`
gate, so a dropped build flag stops a pipeline instead of shipping silently.

**[llvm-hardeningpass](https://github.com/IliasSoultana/llvm-hardeningpass)** · C++
The same question one stage earlier. An LLVM module pass that reads SSP,
SafeStack and ShadowCallStack attributes per function at IR level, before the
linker exists. It catches what the ELF scanner cannot, since a binary can carry
canary machinery while individual functions go uninstrumented.

**[diversity-poc](https://github.com/IliasSoultana/diversity-poc)** · Python, C
Two takes on software diversity. `divcc` shuffles link order so each build is
structurally unique; then I measured with emproof's Nyxstone how little that
actually costs an attacker at the gadget level, and it is not much. So the repo
also rewrites the *finished* binary in place, swapping instructions for
equal-length equivalents, each substitution verified by running the result.
Reading a binary, then changing one.

**[elfharden](https://github.com/IliasSoultana/elfharden)** · Go ·
**[elfharden-rs](https://github.com/IliasSoultana/elfharden-rs)** · Rust
The ELF scanner written twice more, against `debug/elf` and `goblin`. A
differential CI job runs all three over the same binaries and fails if they
disagree. That check once caught the Python version calling every shared library
position-independent, which is exactly why it exists.

**[telemetry-stack](https://github.com/IliasSoultana/telemetry-stack)** · Helm, k3s
MQTT broker, exporter, Prometheus and Grafana as one chart, deployed to k3s with
`kubeconform` validation in CI.

---

### Elsewhere

An internship at Fraunhofer IMS had me writing ESP32-S3 firmware under FreeRTOS.
Its update path authenticated images with a plain SHA-256 checksum, which proves
a file arrived intact but says nothing about who sent it; anyone reaching the
broker could publish their own firmware to the fleet. I closed it with an HMAC
signature the device checks before it downloads anything. Nobody asked me to
look, and that habit of reading a machine more honestly than it presents itself,
whether a stripped binary, a firmware update, or an AI agent that can be talked
past its limits, is the thread through all of this.

📍 Hagen, Germany · smilsou1@unimail.tu-dortmund.de
