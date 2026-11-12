# Verification certificate

## Claim

- The numbers of square-symmetry classes of inclusion-maximal no-three-collinear subsets at n=1..9 are `1, 1, 6, 56, 758, 14798, 306727, 8319524, 232764015`.

## Evidence

| What | Program | Author and date | Coverage | Result |
|---|---|---|---|---|
| Producer | `programs/fixed_profiles.c`, `programs/burnside.py` | Lab fixed-profile enumerator, 2026-11-03; adapted and combined by OpenAI Codex, 2026-11-13 | All eight group elements n<=7; seven nonidentity elements n=8,9; saved identity profiles n=8,9 | Values above; each size has integral Burnside quotient |
| Independent enumeration | `verification/canonical.py` | OpenAI Codex, 2026-11-13 | n=1..5 | Agrees in each case |

The canonical checker shares no code or input data with the fixed-cycle producer. Both implement the same determinant definition and square group. The checker directly stores canonical representatives of every maximal set; it does not use Burnside's lemma. Both test maximality under adding a single point. At n=8 the saved identity profile was independently replayed by row and determinant programs in the companion size-profile repository. At n=9 the saved profile is a historical report of two agreeing traversals.

## Replayed for this repository

2026-11-13, Apple Silicon MacBook Air, Darwin arm64. The C program was compiled with `cc -O3 -std=c11 programs/fixed_profiles.c -o /tmp/c3_maximal_fixed`, then invoked for n=1..7 and for n=8,9 with `--nonidentity`, as in the README. `python3 verification/canonical.py` and `python3 programs/burnside.py` were run. Full output and per-symmetry results are in `verification/logs/`. The independent canonical output for maximal sets is `1, 1, 6, 56, 758`. The replayed n=8 and n=9 nonidentity profiles match the historical profiles cell by cell. The full n=8 eight-element replay was done in the companion all-subsets repository; its log is copied here and was not rerun in this repository.

## Not covered

No independent canonicalization was run for n>=6. The fixed-set counts beyond n=5 have only the fixed-cycle implementation, although conjugacy, Burnside integrality and labelled identity counts provide checks. The n=9 identity enumeration was not replayed here. Historical results are not upgraded into a newly replayed independent verification.

## Guide's independent check

pending

## Verdict

partial — independent class enumeration covers n=1..5; n=6..9 needs independent checking of the symmetry fixed-set counts and n=9 needs replay of the identity traversal.
