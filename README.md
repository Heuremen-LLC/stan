# STAN

STAN is a small open-weight model that Heuremen LLC is training to apply its open standard, Faults and Guards 2.0 (https://indahl.ai/standard). Given the title and abstract of a published claim about an AI or quantum measurement result, it drafts the claim-level checklist F1 to F7 for a person to confirm. It is a sorter. It is never a gate or a certificate.

Live status: https://indahl.ai/iris/lab (the STAN section, with the live feed at https://indahl.ai/iris/lab/stan.json).
The standard: https://indahl.ai/standard
Results as data on Hugging Face: https://huggingface.co/datasets/indahl/stan-results

## How it is trained

Three teacher models label each claim blind. They then see each other's labels and label again (crosstalk). Where all three agree on a code and the label is grounded in a quote from the abstract, the claim becomes silver training data. The base model is Qwen3-1.7B (Apache-2.0), tuned with LoRA.

The answer key is the human recounts of published studies. It is split into a development half and a test half. The development half picks the checkpoint and checks that the output parses. The test half is read once, for a paired comparison of STAN against the untrained base, under the rule fixed in PLAN.md.

## What is in this repository

- `PLAN.md`, `PLAN_ADDENDUM_1.md`, their `.sha256` files and OpenTimestamps `.ots` proofs. The plan was committed before any teacher labelled anything and before any score was read.
- `scripts/`: the pipeline code.
- `results/`: numbers only, updated as the run goes (about every 20 minutes when something changes). `live.json` is the same feed the lab page reads.
- `CHECKS.md`: the check block carried by each public reading.

## What is not in this repository

The claim texts, the teachers' raw outputs, the training rows, the answer key's labels and the adapter weights stay private. The claim texts are third-party abstracts, and weights can carry their training text.

## Licence

Free to read, run and cite with attribution (Heuremen LLC, with a link to https://heuremen.org). Use to train or fine-tune AI models is not permitted. See LICENSE.
