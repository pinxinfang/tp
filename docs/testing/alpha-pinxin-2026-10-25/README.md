# Pin Xin — TutorLink v1.4 alpha testing

Tested on 25 October 2026 using the current public `TutorLink.jar` in separate disposable folders and synthetic student records.

## Artifact and environment

- Release: https://github.com/AY2627S1-CS2103T-T13-4/tp/releases/tag/v1.4
- JAR SHA-256: `61462cbb34c3b7c8047904c8d000e6e759270dcb27a313a41d0581c4784aec5d`.
- This matches GitHub's current asset digest, but differs from the release's downloadable checksum manifest.
- Advertised release source: `0d0d48e7c49e10742a93cc0907e8c588d8bdb70d`. The downloaded JAR includes the later three-column workspace, so the artifact hash is the authoritative identity for these results.
- macOS 15.7.3, x86_64; Azul Zulu OpenJDK 25.0.3+9-LTS, JavaFX distribution; assertions enabled with `-ea`.
- Tested groups: add/optional contact details/remark; deletion confirmation/followup/followups. Recent feature history attributes optional contacts/remarks to Zhiyuan and deletion/followups to Deron. Pin Xin's own search implementations were not evaluated as assigned feature groups.

## Method

A local Java instrumentation agent submitted commands through the released application's real JavaFX command box. The JAR's entry point, production classes, UI, parser, model and storage were used unchanged. Screenshots are snapshots of the real rendered application scene, not mockups. Commands, feedback, displayed records, selected index, UI labels and saved JSON were recorded after each step.

The initial workflow ran independently before checking the repository for duplicate reports. No existing alpha-bug reports were found at the time of comparison. Comparison with Xiuyuan's and Zhenyao's independent results remains for the team; this record does not claim that they have tested these findings.

## Coverage

- 62 baseline UI steps passed their expected error-state and record-count checks.
- 3 restart checks passed. Full saved-roster JSON matched before and after restart, including remarks, follow-up state and deletion.
- 56 additional exploratory/reproduction steps completed (28 boundary cases, 10 further workflow cases, 18 focused reproduction steps).
- Rejected inputs preserved the saved roster. Normal add with omitted or populated contact details, case normalization, duplicate rejection, missing/invalid fields, remark set/replace/clear, literal prefixes in remarks, follow-up mark/repeat/complete, full-roster follow-up listing, invalid indices/actions, delete preview/abandon/confirm, and deletion in sorted results were exercised.
- Long remarks and contact details remained scrollable/wrapped. A suspected email-validation hang did not reproduce and is not reported as a bug.
- Local runtime coverage is Intel macOS only. No Windows/Linux or ARM64 execution is claimed.

## Findings submitted for triage

1. Email aliases containing adjacent permitted special characters are rejected despite satisfying the displayed constraints.
2. Email local parts longer than the standard 64-octet boundary are accepted and persisted.
3. Optional phone/email/address cannot be returned to `Not provided` through the CLI. This is a contact-lifecycle feature flaw, not a claim that the guide currently promises empty-prefix clearing.
4. Deletion preview can name one student while another remains highlighted and displayed in Student Details. This is a usability finding; confirmed deletion itself used the correct displayed index.
5. The published checksum manifest does not match the current released JAR. This is an incidental release finding in addition to the assigned feature testing.

## Evidence

- `normal-results.json`: baseline commands and observations.
- `restart-results.json`: restart observations.
- `confirmed-results.json`: focused application reproductions.
- `valid-email-rejected.png`, `oversized-email-accepted.png`, `contact-cannot-clear.png`, `delete-preview-mismatch.png`: application screenshots.
- `release-checksum.txt`: downloaded artifact versus published manifest.

All `clear` commands in this record operate on disposable synthetic-data folders. The user's working roster and source branch were not modified.
