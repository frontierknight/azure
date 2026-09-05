<div align="center">

# Azure Knight 🔵

**The blue-team / defensive-security agent of [Frontier Knight Labs](https://github.com/frontierknight).**

*SOC + DFIR persona · 8-phase response chain · executes Kali-native tools · offline · built for Kali.*

Runs on [pi](https://pi.dev) · red-team counterpart: [Crimson Knight 🔴](https://github.com/frontierknight/crimson) · proving ground: [Knightfall](https://github.com/frontierknight)

</div>

---

Azure Knight is a defensive-security agent: it selects the right workflow from a bundled library of **370 defense skills** (from the [Anthropic Cybersecurity Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills), Apache 2.0), checks the toolchain it needs, then **actually runs the Kali-native tools** (Volatility, YARA, Sigma, Zeek, Suricata, Splunk, …), reads the real output, and reasons forward — one phase at a time, at your pace. It runs as a pi extension and leaves plain `pi` untouched.

## Install

Needs [pi](https://pi.dev) (Node ≥ 22) and a model configured in pi (`pi` once to sign in).

```bash
git clone https://github.com/frontierknight/azure ~/azure
cd ~/azure && ./install.sh
source ~/.zshrc
azure
```

The installer sets up an isolated config, wires the `azure` command, checks your Kali toolchain (prints `apt install` for anything missing), and drops an optional API-keys template at `~/.frontierknight/keys.env`. On Kali the defensive tools are mostly already there.

## How it works — one phase at a time, you set the pace

```
/engage <scope>    lock the scope — asks you to confirm authorization
/engage            (no arg) confirm authorization → runs phase 1, then STOPs
/next              advance one phase (it summarizes, then waits for you again)
/report            jump to the report
```

**8-phase defense (IR + threat hunting):**
`DETECT → TRIAGE → HUNT → INVESTIGATE → CONTAIN → ERADICATE → HARDEN → REPORT`

Nothing runs against a system until you confirm authorization. Each phase then **runs** its tools, reads the output, and stops for your `/next`.

**8 defensive tools:** `incident_response`, `threat_hunt`, `malware_analysis`, `forensic_analysis`, `detection_engineering`, `security_hardening`, `compliance_audit`, `cloud_security_audit`

## Commands

| Command | Does |
|---------|------|
| `/engage <scope>` · `/next` · `/phases` · `/report` | Start · advance · show the chain · report |
| `/find <query>` | Semantic skill search — also by ATT&CK id (`/find T1003`) |
| `/log <note>` · `/ioc [item]` | Add a finding to the evidence chain · record an IOC |
| `/evidence` · `/reset` | Show the full incident memory · clear it |
| `/arsenal [kw]` · `/help` | Browse skills · how to use |

Memory (scope, phase, evidence chain, IOC ledger) persists to `.azure.json` in the working dir and survives restarts.

## Rules of engagement

Operate **only on systems you are authorized to defend**. A two-step `/engage` gate enforces authorization before anything runs. These agents execute real commands — use responsibly.

## License

MIT (extension code). The bundled skills are Apache 2.0 by their authors.
