# cloud-itonami-lei-9695002oy2x35e9x8w87

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Ipsos SA.**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Ipsos SA**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Ipsos SA
- **LEI (ISO 17442)**: [9695002OY2X35E9X8W87](https://search.gleif.org/#/record/9695002OY2X35E9X8W87) (GLEIF-verified)
- **Jurisdiction**: FR
- **Website**: https://www.ipsos.com
- **Ticker**: IPS (Euronext Paris)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
