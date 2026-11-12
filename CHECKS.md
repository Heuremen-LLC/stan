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

## 2026-11-12 18:00 STAN v1 paired test on gold test, read once (final.py), not kept
- I: holds: keep rule, interval and seed fixed in PLAN.md before any teacher call (committed and stamp submitted), checkpoint chosen by valid loss before any dev or test output, gold test read once by final.py which refuses a second run
- II: holds: flips counted item by item before netting, STAN right and base wrong 24, base right and STAN wrong 13, pooled over codes, per-code intervals printed
- III: holds: signed per-code differences printed separately, F5 is negative (-0.011), no sum claimed beyond the pre-registered pooled mean
- V: holds: paired bootstrap, 2000 resamples over items, seed 7, 95 percent percentile interval, named in the plan
- VI: holds: the pooled interval [0.000, 0.0346] reaches zero, so the reading is CANNOT_TELL (STRADDLES_EDGE) and the rule says not kept
- R: holds: numbers read from stan/results/paired_test.json
- caught: STAN answers CANNOT_TELL on every code of every item (decided share 0), so its agreement is the majority-class rate. It sorts nothing. Said on the page
- cannot tell: input is title and abstract only while the gold labels came from full-text reads, so abstract-only models may be unable to see what the recounts saw

## 2026-11-12 18:30 Lab headline changed to the decided share (Sage break 1), agreement headline withdrawn
- I: holds: the decided share counts a call as decided when it is PRESENT, ABSENT or NOT_APPLICABLE, the same definition score.py used before any result
- II: holds: per-code shares are kept in the source files, the pooled share is n-weighted over seven codes
- III: caught: the earlier agreement headline counted CANNOT_TELL as agreeing with an unflagged recount, a fold. Withdrawn from the page, rows stan.baseline.base and stan.baseline.majority withdrawn
- V: holds: a plain share with its count of calls printed, no interval claimed
- VI: n/a: descriptive share, not a stated-against-delivered comparison
- R: holds: read from stan/results/decided_summary.json, written by decided_summary.py from baseline_dev.json and paired_test.json
- cannot tell: whether the models abstain because the abstract lacks the evidence or because they cannot apply the codes. Sage's ceiling check decides it before v2
