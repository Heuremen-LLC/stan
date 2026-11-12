# Check blocks (watch/readcheck.py). One entry per reading, appended, never edited after commit.

## 2026-11-12 12:05 LAB headline: the untrained base model's agreement with the answer key on gold dev (F1 to F7 pooled), against the pooled majority-class rate
- I: holds: the untrained base model Qwen3-1.7B is the none arm, scored on the same 97 gold dev claims and the same seven codes as the three teachers, with the same agreement rule (predicted PRESENT equals gold PRESENT); 679 code calls pooled, 463 agree, nothing dropped, parse failures counted as disagreement
- II: n/a: one pass per model and claim, no repeated item and no flips between runs are claimed
- III: holds: agreement is unsigned and pooled over seven codes by summing agreements and calls; the majority-class rate is the n-weighted mean of the seven per-code rates and every per-code rate is also in baseline_dev.json
- V: holds: two rulers side by side, the model's agreement and the always-guess-the-commonest-answer rate per code, both read from stan/results/baseline_dev.json by code, with the Wilson 95 percent interval on the agreement only
- VI: n/a: the headline reads a baseline, not a comparison of STAN with anything, and the paired test against base on gold test is run once later under PLAN.md
- R: holds: every number is computed from baseline_dev.json by watch/headlines.py lab(), none typed, plan sha256 a6a7ea11 committed before any label was read, dev half of the answer key only, test untouched
- caught: base answers CANNOT_TELL for most codes, so its agreement mostly reflects the share of claims where the answer key says not present, which is why the majority-class rate sits above it for six of seven codes
- cannot tell: the answer key was made from full text and released files while every model here sees only the abstract, so how much of the gap to the answer key an abstract could ever close is not known
