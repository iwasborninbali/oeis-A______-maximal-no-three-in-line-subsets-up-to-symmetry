# OEIS candidate (no A-number yet): maximal no-three-in-line subsets up to symmetry

<!-- oeis-status:begin -->
**OEIS status: not submitted; no A-number yet** (lab registry, 13 Nov 2026).

- A______, maximal no-three-in-line subsets up to the symmetries of the square: **candidate** (2026-11-13: repository built (core c3)). Certificate: partial.

Rules and the full registry: [athanor-oeis](https://github.com/iwasborninbali/athanor-oeis/blob/main/REGISTRY.md).
<!-- oeis-status:end -->

## Definition

For n >= 1, a(n) counts inclusion-maximal subsets of {0,...,n-1}² with no three distinct points collinear, modulo the eight rotations and reflections of the square. The offset is 1. Maximal means that adding any individual unselected grid point creates a collinear triple; the unique singleton is maximal for n=1.

## Terms / result

| n | a(n) |
|---|---:|
| 1 | 1 |
| 2 | 1 |
| 3 | 6 |
| 4 | 56 |
| 5 | 758 |
| 6 | 14798 |
| 7 | 306727 |
| 8 | 8319524 |
| 9 | 232764015 (partly based on a historical full count) |

## How it was obtained

For each square symmetry, the producer enumerates unions of its cell cycles and checks both collinearity and maximality on the full grid. Maximality tests the addition of one arbitrary grid point, not just an orbit of points. Burnside's lemma gives the number of classes as one eighth of the sum of the eight fixed-set counts. The n=9 identity profile comes from the lab's historical full-grid enumeration; its seven other profiles were replayed here. The full n=8 fixed-set run was replayed in the companion repository, and two other programs replayed its identity profile in the companion size-profile repository.

## Verification

A separate program enumerates all safe subsets and canonicalizes each maximal one for n=1..5; it agrees with the Burnside result. The n=6..9 fixed-set counts lack an independent orbit enumeration, and n=9's identity count was not replayed here. See [CERTIFICATE.md](CERTIFICATE.md).

## Prior art and credit

[A398184](https://oeis.org/A398184) counts labelled maximal sets, and [A000769](https://oeis.org/A000769) concerns only 2n-point solutions up to symmetry. The lab's previous work computed fixed-set profiles at n=8 and n=9. See [PRIOR-ART.md](PRIOR-ART.md).

## Reproduce

Requires a compiler supporting `unsigned __int128` (Clang or GCC) and Python 3. On the test machine the n<=7 fixed-set replay takes a few seconds, canonicalization through n=5 takes a few seconds, and each n=8,9 nonidentity replay takes under a second.

```sh
cc -O3 -std=c11 programs/fixed_profiles.c -o /tmp/c3_maximal_fixed
for n in 1 2 3 4 5 6 7; do /tmp/c3_maximal_fixed "$n" > "verification/logs/fixed-n$n.jsonl" 2> "verification/logs/fixed-n$n.stderr"; done
for n in 8 9; do /tmp/c3_maximal_fixed "$n" --nonidentity > "verification/logs/fixed-n$n.jsonl" 2> "verification/logs/fixed-n$n.stderr"; done
python3 programs/burnside.py
python3 verification/canonical.py
```

Expected output is in `verification/logs/burnside.txt` and `verification/logs/canonical.txt`. Replaying into the tracked logs changes timing fields; discard those changes before committing. The Burnside script combines the replayed nonidentity profiles with saved identity profiles for n=8,9.

## Provenance

The fixed-cycle program and profiles derive from `athanor-foundation/instruments/hammer`, commit `204d667842829e1c15ca2ee23210e86f99835e2d`: `hammer/core/workspace/oeis-row8/fixed_profiles.c`, `fixed-n8.jsonl`, `fixed-n9.jsonl`, `n8.json` and `n9.json` under that workspace folder. The fixed-profile program was adapted to include the identity and to provide `--nonidentity`. Burnside and the independently written canonical checker were copied from the companion `oeis-A______-no-three-in-line-subsets-up-to-symmetry` at commit `780c77d`; the n=8 complete run log was also copied from there. No archive DOI has been established for these specific files.

## Author, licence

Aleksei Kudriashov (ORCID 0009-0006-8885-5338), Athanor lab, with AI assistance (OpenAI Codex cores; Claude Code as the lab's guide). Code: MIT; data and text: CC BY 4.0 (see LICENSE.md).
