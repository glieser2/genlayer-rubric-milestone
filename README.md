# RubricMilestone v3.2

A standalone GenLayer Intelligent Contract for client-controlled acceptance of a fixed software delivery. It transfers no assets.

This repository is the contract-specific **source distribution** of RubricMilestone, extracted from [the canonical development repository](https://github.com/glieser2/genlayer-evidence-primitives/tree/06819fba7239266cc9aa8dd51781295d3a2f45d7). It is the same implementation and contribution, not a new contract version. Shared regression tests and historical CI remain in that canonical repository. SourceQuorum is a separate primitive and is not included here.

## Review the primitive

- [Contract source](rubric_milestone.py)
- [Detailed design and configuration](CANONICAL_README.md#rubricmilestone)
- [Preserved verification record](TESTING.md)
- [Preserved live transaction and final-state record](LIVE_VERIFICATION.md#rubric-v32-finalized-verification)
- [Security history and limitations](SECURITY.md)
- [Source and documentation provenance](PROVENANCE.md)

Before the worker submits, the client commits criterion text, exact ordered quotation anchors, file hashes and CI policy. Validators inspect the Git tree, reject unpinned executable/configuration changes, verify the pinned hashes, and bind a successful CI workflow/job/step to the delivery commit and repository.

The contract deterministically chooses a unique shortest 10..500-character quotation containing the committed anchors in order. Validators recompute the quotation and offset. A citation-only semantic assessment and a separate full-context assessment must agree. Missing or ambiguous evidence yields UNCLEAR/NEEDS_EVIDENCE. Permanent gate failures yield REJECTED; transient network or pending-CI failures can retry. Only the client can authorize revision or finalize the exact current revision/digest. Submission and review history remain available.

This accepts a reviewed, fixed implementation: inspect every policy-pinned file before deploying. Phrase inclusion does not prove truth; model judgments can still be wrong.

## Reproduce the shared regression suite

Use Python 3.13. The complete official-SDK harness includes regression fixtures for both primitives, so run it in the pinned canonical checkout, not in this source-only distribution:

```sh
git clone https://github.com/glieser2/genlayer-evidence-primitives.git rubric-verification
cd rubric-verification
git checkout 06819fba7239266cc9aa8dd51781295d3a2f45d7
python -m venv .venv
# Linux/macOS:
. .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
python -I -m pip install -r requirements-test.txt
python -I -X utf8 scripts/run_tests.py
python -I -X utf8 scripts/check_contracts.py
```

Compare this distribution's rubric_milestone.py with contracts/rubric_milestone.py in the canonical checkout before attributing a run to this distribution. Expected SHA-256: `7dcadd8f6fa018442f3cad0ad1e1ef36ddcfbc4ae19ca01b9f773bd82deab75b`.

The Direct Mode suite mocks HTTP and model responses. Historical Rubric v3.2 verification passed 117/117 tests and GenVM checks in [canonical CI run 41368479862](https://github.com/glieser2/genlayer-evidence-primitives/actions/runs/41368479862) at code commit 298d4f077b378a6886d399b301426979b0609bc0. Later shared-suite changes are documented separately in the pinned canonical records. No new independent test or audit is claimed by publishing this distribution.

## Inspect the deployed instance

[Studionet contract 0xA74Ad94c232986d1959a826cff64500Ed7b069FE](https://explorer-studio.genlayer.com/address/0xA74Ad94c232986d1959a826cff64500Ed7b069FE).

The preserved [live verification record](LIVE_VERIFICATION.md#rubric-v32-finalized-verification) links evaluation and application finalization transactions and records FINALIZED / APPROVED with the exact review digest. The deployment was made from the canonical repository before this distribution was created. Historical CI, policy commitments, delivery submissions and transaction URLs continue to identify that original repository.

Finite tests and live examples do not establish universal correctness or guarantee a contribution score.
