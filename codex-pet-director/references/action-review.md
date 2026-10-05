# Action Review And Revision

Review the generated result, not just the plan. Use the approved production base as the character reference. Default to reviewing 2–3 completed action rows together in one pass: inspect their exported active frames at intended display size and available playback. Cover all frames within that pass; do not split QA into mandatory per-frame approval rounds, key-pose review, slow-playback review and repeated final review.

Check four practical things:
- The same character: recognizable face, proportions, clothing, colors, material/texture, shading and style across this batch and the approved reference. Material must remain visibly consistent; microscopic texture identity is not required. Natural perspective, occlusion and expressions are allowed.
- Clear frames: no obvious blur, extra or detached body parts, clipping or overlap; clean background/transparency and stable overall scale.
- Readable action: movement looks connected and intentional. An ordinary run should visibly alternate legs and have natural arm coordination; other performances follow their own intended movement. Do not require a fixed frame-by-frame gait template.
- Usable sequence: frame count and layout match the official state; loops join reasonably where intended.

Reject visible defects that materially change the character or break the action. Do not fail a plausible animation because it differs from a suggested pose plan, has small texture differences, or uses valid stylized timing. If a hidden limb or subtle detail cannot be judged, record uncertainty instead of guessing a failure. Do not add repeated review rounds for minor preferences.

Record `actions.<state>.qa` with `status` (`unreviewed`, `pass`, `fail`), `artifact`, and brief `issues`. If playback is unavailable, say that motion playback remains unverified; a structural script pass is not a visual pass.

Show all 2–3 actual rows/animations together with one short batch summary and offer accept batch, redo named actions, or continue. Record per-action results from this single review for artifact tracking, not as extra user approval steps. User-requested angle, amplitude or acting changes are revisions, not evidence of technical failure. Paired left/right runs use matching mirrored angles by default: equal profile/three-quarter turn, camera elevation and scale. Check them together in the existing batch review; on a single-direction redo compare with its accepted counterpart without re-reviewing that whole action. Preserve asymmetric details on the correct anatomical sides. Unequal angles are allowed only when requested.

On redo, set affected QA to `unreviewed` and `preview_confirmed=false`. Review only the changed artifact using the same four checks before replacing an accepted version. Preserve unaffected actions and their current review results. Aggregate visible problems into one targeted correction; if it still fails, show the issue and next options instead of repeating automatically. User acceptance never implies an unperformed inspection occurred.

At final assembly, run the structural format check and a single cross-batch material/style/scale comparison. Reuse the batch motion reviews. Reopen visual QA only for rows actually changed by assembly/extraction or a shared-base/alignment edit. This keeps routine QA to one pass per batch plus one pass on a targeted correction; never waive review of a newly generated replacement.
