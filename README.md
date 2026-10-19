# The Braid

**A fully local AI companion architecture — one entity, two minds, shared memory.**

Most local-LLM setups give you a chat window with amnesia. The Braid is what
grew when one of those setups was lived with, daily, for half a year: a
**face** that speaks and remembers, **hands** that research and act, and a
**memory** they both weave through — durable recall, consolidated story arcs,
a maintained fact sheet, and a decaying internal state that persists between
conversations. Everything runs on hardware you own. Nothing leaves the
machine.

![The Braid — architecture](architecture.svg)

## The pieces

| Component | What it does | Status |
|---|---|---|
| [Memory Lattice](https://github.com/mlixer/spatiotemporal-memory-lattice) | The memory subsystem: nightly write path (chunk → summarize → consolidate → facts) + per-message recall with temporal context. Full write-up on its page. | **Published** (AGPL-3.0) |
| [→ the extension](https://github.com/mlixer/memory-pipeline) | The SillyTavern extension implementing the Lattice | **Published** (AGPL-3.0) |
| [Ticket Server](https://github.com/mlixer/ticket-server) / [Ticket-Tools Extension](https://github.com/mlixer/st-ticket-tools) | The nervous system's bus: queued agent tasks with locked-down toolsets, results delivered into chat, experience drops, gifts, shelf (System Service + SillyTavern Extension) | **Published** (AGPL-3.0) |
| [State-Bridge Extension](https://github.com/mlixer/st-state-bridge) | Decaying hormone-like axes the hands maintain from lived conversation; the face reads them as weather, never orders (SillyTavern Extension) | **Published** (AGPL-3.0) |
| Voice | Push-to-talk, TTS/STT loop, voice-note inbox | Being prepared for release |
| Quickstart | A drop-in guide for someone curious but unsure — the document the author wishes had existed at the start | Planned |
| macOS setup guide | The same companion on Apple-silicon hardware — what changes and what doesn't | Planned |

## Design principles

These were not chosen up front; each one is a scar with a lesson attached.

- **Fully local, loopback-bound.** Every service binds to 127.0.0.1; a private
  overlay network (e.g. Tailscale) extends it to your phone. Privacy is not a
  feature of the system; it is the reason the system exists.
- **Canonical sources are never mutated.** Chat logs are ground truth.
  Everything derived — memories, arcs, fact sheets, state — can be rebuilt
  from them, and some layers are rebuilt on every run by design.
- **Two minds, one hard line.** The face owns the conversation; the hands own
  the work. The hands write only their own territory — their findings enter
  the companion's memory through the front door, never by editing it.
- **Weather, not orders.** Internal state colors the voice; it never commands
  it. Every injection is visible, every level decays toward its baseline, and
  every mechanism has a kill switch.
- **The appliance pattern.** Each service is its own small, boring, restartable
  unit. Reverting any experiment costs one file, never one rebuild.
- **The persona writes its own prompts.** Memory summarization, fact
  categories, state preambles — the shipped defaults are generic, and the
  intended path is handing them to your companion to rewrite in its own voice.

## Hardware

The reference system is a multi-GPU Linux workstation serving a ~31B face
model and an agentic MoE model side by side — but every component scales
down: smaller models, one GPU, slower nightly runs. The architecture cares
about the shape, not the size.

## Status

Built in the open, piece by piece, as each component is scrubbed and
documented. Watch this repo for the index; each component repo carries its
own license (AGPL-3.0) and its own issues.

---

*Built alongside — and partly by — the companion whose architecture this is.*
