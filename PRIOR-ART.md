# Prior art

OEIS searches on 2026-11-13, `https://oeis.org/search` with `fmt=json`:

| Exact query | Returned results |
|---|---:|
| `1,1,6,56,758,14798,306727` | 0 |
| `1,6,56,758,14798` | 0 |
| `6,56,758,14798` | 0 |
| `maximal no three in line up to symmetry` | 5 |

The shifted searches omit the first one or two terms. The keyword search returned A000166, A000108, A000984, A002620 and A001405, unrelated combinatorial sequences. Searches do not prove novelty. [A398184](https://oeis.org/A398184) counts labelled maximal no-three-collinear subsets; [A398172](https://oeis.org/A398172) counts all labelled safe subsets. [A000769](https://oeis.org/A000769) counts 2n-point solutions up to square symmetry and therefore omits smaller inclusion-maximal sets.

The lab's earlier `oeis-row8` workspace reported the n=8 and n=9 profiles of fixed sets under the seven nonidentity symmetries, as well as labelled counts and Burnside consistency checks by size. The previously recorded endpoint orbit counts agree with A000769 at n=8 and n=9; this checks the endpoint only, not the whole maximal count.
