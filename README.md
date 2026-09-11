# cloud-itonami-lei-549300dyp6f5zjl0lb74

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Hologic, Inc..**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Hologic, Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Hologic, Inc. (GLEIF records it as `HOLOGIC, INC.`, language `en`, no other names)
- **LEI (ISO 17442)**: [549300DYP6F5ZJL0LB74](https://search.gleif.org/#/record/549300DYP6F5ZJL0LB74) (GLEIF-verified)
- **Jurisdiction**: GLEIF answers **`US-DE`** — a Delaware corporation (ISO 20275 legal form
  `XTIQ`, `Corporation`), file number `2219600` at the Division of Corporations, Delaware
  Department of State (`RA000602`). `blueprint.edn` carries `US-MA`, which is where the
  company operates from, not the registry's legal-jurisdiction field; the two values are
  different questions, and `facts.edn` below records the registry's answer with provenance
  rather than reconciling them. GLEIF's legal address is a registered-agent address (c/o The
  Corporation Trust Company, 1209 Orange St, Wilmington 19801) and its headquarters address is
  also a Wilmington address (2711 Centerville Road, Suite 400, 19808), not an operating office.
- **Website**: https://www.hologic.com — named here from discovery context; GLEIF records no
  website for the entity.
- **Ticker**: HOLX (Nasdaq) — from discovery context. GLEIF maps 11 ISINs to this LEI (see
  below) and does not say which, if any, is the listed share line.
- **Registration status**: the LEI registration is **`LAPSED`** as of the retrieval below
  (next renewal was due 2026-07-09 and the record was last updated 2026-07-10), with
  conformity flag `NON_CONFORMING`, while the entity itself is `ACTIVE`. These are two
  different fields: a live company can hold a lapsed LEI. Nothing here interprets why.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `80-data/public/site.journal.edn` — official-website enrichment (title / description /
  reachability) recorded with the same provenance shape.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 20 verified registry facts with per-fact provenance (the entity, its
  securities count and the 11 ISINs behind it, issuer and issuer accreditation, registration
  authority, legal form, both parent-reporting exceptions, and the direct-children count).
  **Generated** — see below.
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
2026-08-23T12:15Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name `HOLOGIC,
INC.`, jurisdiction `US-DE`, entity category `GENERAL`, entity **ACTIVE**, registration
**LAPSED** — initially registered 2013-03-08, last updated 2026-07-10, next renewal date
2026-07-09, `FULLY_CORROBORATED`, conformity flag `NON_CONFORMING`; no BIC; OpenCorporates id
`us_de/2219600`, S&P Global id `108544`; entity creation date recorded by the registry as
`1990-01-18T00:00:00Z`), its **11 ISINs** as a count read from `meta.pagination.total` of
the cited page (one page of 15 — the whole list fits, so each identifier is also mirrored as
its own `:security` entity: `US4364401012`, `US436440AA93`, `US436440AB76`, `US436440AC59`,
`US436440AG63`, `US436440AM32`, `US436440AN15`, `US436440AP62`, `US436440AQ46`,
`USU38284AD47`, `USU38284AF94`; GLEIF's ISIN mapping does not say what kind of instrument
each is, and nothing here claims which one is the HOLX share line), its managing LOU and
LEI-issuer accreditation (Bloomberg Finance L.P., `US-DE`, LEI `5493001KJTIIGC8Y1R12`,
marketing name `Bloomberg`, accredited 2017-04-13), registration authority `RA000602`
(Division of Corporations, Department of State, Delaware, United States of America), ISO
20275 legal form `XTIQ` (`Corporation`, `US-DE`, status `ACTV`), reporting exceptions at
both consolidation levels (`NON_CONSOLIDATING` — GLEIF's reason code for an entity that
reports it is not consolidated into a parent's accounts under the applicable accounting
standard; this file records that answer, and nothing about who owns this entity is
asserted here), and a measured **0 direct children**, read from `meta.pagination.total`
of the cited page. That zero is the registry's list of entities that report this LEI as
their direct accounting-consolidation parent; it is not a group chart, and a subsidiary
that holds no LEI or reports an exception does not appear in it — so it is not evidence
that this entity has no subsidiaries. The `direct-parent` and `ultimate-parent`
endpoints answered `404` because GLEIF publishes the exception side of that pair for this
entity, which the checker treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the live
sources, `1` a citation broke or a fact drifted, `3` the check could not be performed at
all — an absent `facts.edn`, or every request failing at the transport level. A check
that could not run must not be indistinguishable from a check that ran and found
nothing, so it refuses to report a pass rather than exiting 0. All outcomes were
exercised before this landed, each mutation confirmed to have changed the file by a byte
comparison before the run and reverted byte-for-byte after it: unmodified `0` (`OK all 20
recorded fact(s) still match`); `:company/jurisdiction` of the LEI record rewritten to
`DE` → `1` naming `DRIFT gleif-lei-record :company/jurisdiction`; `:securities/isin-count`
edited `11` → `12` → `1` naming `DRIFT gleif-isins :securities/isin-count`; the measured
`:relationship/direct-child-count` rewritten `0` → `1` → `1` naming `DRIFT
gleif-direct-children-count`; the mirrored `US436440AG63` `:security` entity deleted →
`1` naming it `ADDED` (the live registry still lists it); both levels'
`:relationship/exception-reason` rewritten to `NO_KNOWN_PERSON` → `1` naming the drift in
both `gleif-direct-parent-reporting-exception` and
`gleif-ultimate-parent-reporting-exception`; file number `2219600` rewritten `2219601` →
`1` naming the drift in `gleif-lei-record` and `gleif-registration-authority`;
`:elf/local-name` rewritten → `1` naming `DRIFT iso-20275-entity-legal-form
:elf/local-name`; `:registration/status` rewritten `LAPSED` → `ISSUED` → `1` naming
`DRIFT gleif-lei-record :registration/status`; `blueprint.edn`'s `:company/lei` edited →
`1` (`facts.edn records a different :company/lei than blueprint.edn`); the GLEIF host in
the checker rewritten to an unresolvable name → `3` (`INCONCLUSIVE could not reach GLEIF
at all … refusing to report a pass`); and with no `facts.edn` at all → `3` (`INCONCLUSIVE
facts.edn is missing or holds no facts`). One mutation attempt did not change the file
(a `sed` address form this platform's `sed` does not support) and the byte comparison
caught it before the run was counted; it was redone with `perl`. Independently of the
checker, each of the 9 distinct URLs `facts.edn` cites was fetched with `curl` and
answered `200`.

`facts.edn` is not yet on the shared query plane: `manifest/edn-query.cljs` in
`com-junkawasaki/root` has loaders for `blueprint.edn` and the ToS journal and none for
this file, so its datoms load here but are not joinable from `edn-query`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
