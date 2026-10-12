# lompi

**The package manager for Loment libraries.** A library is a *directory*, its identity is a
**content hash**, and its dependencies are the `use` lines in the source. lompi is written
**in Loment** and built by the Loment toolchain.

**It is a standalone command, not a `loment` subcommand**: `loment help` does not list it; you
run `lompi` directly.

## Building it

You need the Loment toolchain first (<https://github.com/FujoJTOP/loment>), then **from this
directory**:

```
loment build lompi.lomt -o lompi
```

(The directory matters: this toolchain resolves relative imports such as `use "lpi_cli.lomt"`
against the **current working directory**.)

```
lompi version
lompi list  [<store>]                     # what is in the store (index is a synonym)
lompi show  [<store>] <name[@version]>
lompi tree  [<store>] <name[@version]>
lompi resolve [<store>] <name[@version]>  # write a lock, pinned by content hash
lompi check <dir>                         # validate a library directory
lompi fetch --registry <url>              # download a registry over http
```

`<store>` is optional — omit it and the **global store** is used (the `store:` line that
`lompi config` prints), the same way `pip` never asks you where site-packages lives.

`fetch` does the download itself when the registry is `http://` with an IPv4 literal: it reads
the index, GETs each file, and **verifies the sha256 the index states**. It will not do
`https://` (there is no TLS in the toolchain) or a hostname (no resolver) — for those it prints
the `git clone` to run and names the piece that is missing.

The self-test driver is `lpi_test.lomt`: one `selftest_<module>()` per module, summarised with
the **exit code as the verdict**.

## What this repository is

**It is the publish outlet of the Loment repository, not a development tree.** Development
happens in <https://github.com/FujoJTOP/loment>, under `lompi/`; this repository is regenerated
from it by that repository's `tools/loment_publish.py`. **Do not commit here** — the next
publish overwrites it.

The guide is `.claude/skills/lompi/SKILL.md`.
