<div align="center">

# 🐞 Ladybug Memory

**Knowledge and intelligence should be separate — so systems can keep learning.**

Graphs are how we represent latent information in a human-legible way.

</div>

---

## Vision

> Intelligence reasons. Knowledge remembers. When the two are tangled together, every update risks what was already learned.
>
> Ladybug Memory separates them: intelligence stays fluid and replaceable, while knowledge accumulates in open, inspectable graphs that both humans and agents can read, query, and trust.

- **Separate to keep learning** — weights and prompts change; facts, entities, and relationships persist. Continuous learning only works when memory outlives the model run.
- **Graphs for latent information** — embeddings hide meaning; graphs reveal it. Nodes and edges make what the system "knows" legible, auditable, and editable.
- **Open formats, zero-copy speed** — memory should move from disk to analytics without conversion taxes or proprietary lock-in.

---

## Featured repositories

### 🧠 [`ladybug-memory-rs`](https://github.com/Ladybug-Memory/ladybug-memory-rs) — the `lbm` tool

Agent long-term memory on LadybugDB, with knowledge-graph extraction running **ONNX-only** — no Python, no torch at inference.

- `lbm` CLI with JSON I/O: `remember` / `search` / `forget` / `tour` / `status` / `review` / `sync` — what pi extensions spawn
- 5-step pipeline: extract → compare → resolve → decide → write — only distilled facts are stored, never raw transcripts
- GLiNER2.5 entity extraction, canonical entities with aliases, conflict review cues, and provenance without message text

```sh
cargo build --release -p lbm
lbm remember "User prefers Python for scripting" --scope project
lbm search "python" --json
```

### ❄️ [`icebug`](https://github.com/Ladybug-Memory/icebug) — frozen graph analytics

A fork of [NetworKit](https://github.com/networkit/networkit) emphasizing **zero-copy columnar storage**. High-performance graph analysis backed by read-only memory — up to 5× more CPU- and memory-efficient on Arrow columnar data.

- Scales from thousands to billions of edges, many algorithms parallel for multicore
- Python module (C++ core via Cython), also usable as a native library
- Reads Arrow tables directly — no copy, no conversion

```sh
uv pip install icebug
```

### 📦 [`icebug-format`](https://github.com/Ladybug-Memory/icebug-format) — the open graph interchange

A proposal for graph standardization, in two flavours that share one CSR layout:

| Format | Storage | Use case |
|---|---|---|
| **icebug-disk** | Parquet files | Object storage, persistence |
| **icebug-memory** | Apache Arrow tables | In-process, zero-copy access |

An icebug-disk graph is just ordinary Parquet files whose columns form a standard CSR array (`target` indices + `ptr` indptr) — readable by anything that reads Parquet, writable by anything that can produce a CSR adjacency. No proprietary lock-in.

```sh
uv run icebug-format --source-db karate_random.duckdb --schema schema.cypher
uv run icebug-format --source-dir ldbc/cit-Patents --backend pyarrow
```

---

## How it fits together

```
┌─────────────────────┐     ┌──────────────────────┐     ┌──────────────┐
│ ladybug-memory-rs   │────▶│ icebug-format        │────▶│ icebug       │
│  lbm remembers,     │     │  open Parquet /      │     │  analytics   │
│  extracts entities  │     │  Arrow CSR graphs    │     │  at scale    │
└─────────────────────┘     └──────────────────────┘     └──────────────┘
        knowledge                 legible interchange          insight
```

Memory captures it. Format stores it openly. Analytics reasons over it — without disturbing what is known.

---

## Sister org

We build alongside our sister org **[Latentpedia](https://github.com/Latentpedia)** — come explore what they're publishing.

---

<div align="center">

🐞 *Remember what matters.*

</div>
