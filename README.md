# cloud-itonami-lei-9695002oy2x35e9x8w87

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Ipsos SA.**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Ipsos SA**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Ipsos SA (GLEIF records it as `IPSOS`, language `fr`)
- **LEI (ISO 17442)**: [9695002OY2X35E9X8W87](https://search.gleif.org/#/record/9695002OY2X35E9X8W87) (GLEIF-verified)
- **Jurisdiction**: `FR` — a French société anonyme with a board of directors (ISO 20275
  legal form `K65D`, `SA à conseil d'administration (s.a.i.)`), SIREN `304555634` in the
  Sirene register kept by INSEE (`RA000189`). GLEIF's legal address and headquarters
  address are the same Paris address (35 rue du Val de Marne, 75013). `facts.edn` below
  carries the registry's answer with provenance.
- **Website**: https://www.ipsos.com
- **Ticker**: IPS (Euronext Paris) — a listing named here from discovery context, not read
  from GLEIF. GLEIF maps **5 ISINs** to this LEI; all five are mirrored in `facts.edn`, and
  nothing there says which of them is the listed share line — GLEIF's ISIN mapping does not
  distinguish equity from debt.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `80-data/public/site.journal.edn` — official-website enrichment (title / description /
  reachability) recorded with the same provenance shape.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 16 verified registry facts with per-fact provenance (the entity, its
  securities count and the 5 ISINs behind it, issuer and issuer accreditation, registration
  authority, legal form, both parent-reporting exceptions, the direct-children count and
  the 2 children behind it). **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind them.
`facts.edn` now carries them as data, and every value in it was read out of a public
registry response whose URL and retrieval time sit next to the value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T11:20Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name `IPSOS`,
jurisdiction `FR`, entity category `GENERAL`, entity **ACTIVE**, registration **ISSUED**
since 2014-02-10 with the next renewal due 2027-03-24, last updated 2026-03-19,
`FULLY_CORROBORATED`, conformity flag `CONFORMING`, BIC `IPSOFRPPXXX`, OpenCorporates id
`fr/304555634`, S&P Global id `135029`, entity creation date recorded by the registry as
`1974-12-31T23:00:00Z`, which is midnight 1975-01-01 in Paris; entity status and
registration status are different fields and are recorded separately), its **5 ISINs** as a
count read from `meta.pagination.total` of the cited page (one page of 15 — the whole list
fits, so each identifier is also mirrored as its own `:security` entity: `FR0000073298`,
`FR00140015R3`, `FR00140078W1`, `FR001400EGG5`, `FR001400WRF6`), its managing LOU and
LEI-issuer accreditation (INSEE — Institut National de la Statistique et des Études
Économiques, LEI `969500Q2MA9VBQ8BG884`, accredited 2018-01-30), registration authority
`RA000189` (Register of Companies — Sirene, INSEE, France), ISO 20275 legal form `K65D`
(`SA à conseil d'administration (s.a.i.)`, `FR`, status `ACTV`), reporting exceptions at
both consolidation levels (`NO_KNOWN_PERSON` — GLEIF's reason code for an entity with no
known controlling person, e.g. a diversified shareholding, so the registry names no parent
at either level; this file records that answer and nothing about who owns this entity is
asserted here), and a measured **2 direct children**, read from `meta.pagination.total` of
the cited page (one page of 15), each mirrored as a `:direct-child` entity: Ipsos Corp.
(`CA-BC`, LEI `254900VXNA8QHXXGOX50`) and IPSOS HOLDING BELGIUM (`BE`, LEI
`549300CXQN6P8PH5R436`), both `ACTIVE`, both `IS_DIRECTLY_CONSOLIDATED_BY` this entity.
That is the registry's list of entities that report this LEI as their direct
accounting-consolidation parent; it is not a group chart, and a subsidiary that holds no
LEI or reports an exception does not appear in it — so absence from this list is not
evidence that a subsidiary does not exist (Ipsos operates in far more than two countries).
The `direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF publishes
the exception side of that pair for this entity, which the checker treats as a fact rather
than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the live
sources, `1` a citation broke or a fact drifted, `3` the check could not be performed at
all — an absent `facts.edn`, or every request failing at the transport level. A check
that could not run must not be indistinguishable from a check that ran and found
nothing, so it refuses to report a pass rather than exiting 0. All outcomes were
exercised before this landed, each mutation confirmed to have changed the file by a byte
comparison before the run and reverted byte-for-byte after it: unmodified `0` (`OK all 16
recorded fact(s) still match`); `:company/jurisdiction` rewritten to `DE` → `1` naming
`DRIFT gleif-lei-record :company/jurisdiction` (and the managing-LOU entity's, which the
same `sed` also hit); `:securities/isin-count` edited `5` → `6` → `1` naming `DRIFT
gleif-isins :securities/isin-count`; the measured `:relationship/direct-child-count`
rewritten `2` → `1` → `1` naming `DRIFT gleif-direct-children-count`; the IPSOS HOLDING
BELGIUM `:direct-child` entity deleted → `1` naming it `ADDED` (the live registry still
lists it); the mirrored `FR0000073298` `:security` entity deleted → `1` naming it `ADDED`;
both levels' `:relationship/exception-reason` rewritten to `NON_CONSOLIDATING` → `1`
naming the drift in both `gleif-direct-parent-reporting-exception` and
`gleif-ultimate-parent-reporting-exception`; SIREN `304555634` rewritten `304555635` →
`1` naming the drift in `gleif-lei-record` and `gleif-registration-authority`;
`:elf/local-name` rewritten → `1` naming `DRIFT iso-20275-entity-legal-form
:elf/local-name`; `blueprint.edn`'s `:company/lei` edited → `1` (`facts.edn records a
different :company/lei than blueprint.edn`); the GLEIF host in the checker rewritten to
an unresolvable name → `3` (`INCONCLUSIVE could not reach GLEIF at all … refusing to
report a pass`); and with no `facts.edn` at all → `3` (`INCONCLUSIVE facts.edn is
missing or holds no facts`). Two deletion attempts that failed to change the file were
caught by that byte comparison and redone — their `0` exits were not counted.
Independently of the checker, each of the 9 distinct URLs `facts.edn` cites was fetched
with `curl` and answered `200`.

`facts.edn` is not yet on the shared query plane: `manifest/edn-query.cljs` in
`com-junkawasaki/root` has loaders for `blueprint.edn` and the ToS journal and none for
this file, so its datoms load here but are not joinable from `edn-query`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
