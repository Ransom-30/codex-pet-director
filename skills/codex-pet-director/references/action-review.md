# Action Review And Revision

Read this guide when generating action previews, reviewing finished rows, or revising an existing pet. Structural script checks do not establish visual or motion quality.

## Independent Left And Right Views

Let the user specify `running-left` and `running-right` angles independently: profile, front three-quarter, rear three-quarter, or another described view. If unspecified, recommend a matched pair and show the choice on the action card. Record each angle in `actions.<state>.view_angle`; include it in `final_direction` and `prompt_notes` so row generation receives it.

Lock facial proportions, eye shape/color/spacing, brows, nose, mouth, hairline, markings, accessories, palette, and anatomical side in `appearance.visual_locks`. Perspective may change visible shape and occlude features; it must not invent, remove, swap, or recolor identity details. A left-side marking remains on the character's left side, not always the screen's left. Do not blindly mirror asymmetric faces, hair, text, equipment, or user-selected unequal angles. Generate those views separately from the same production base and identity locks.

## Motion And Frame QA

Review every generated action, including both movement directions and any jumping or turning. The official `running` slot is a working state; evaluate the intended performance rather than forcing a legged run. Adapt checks to floating, sliding, or other explicitly chosen locomotion.

Inspect every active frame in a contact sheet at native 192x208 size and with nearest-neighbor enlargement, then watch the row animation for several loops. Compare both directional rows against the production base and each other. If images or animation cannot be inspected, record `unreviewed`; do not claim a visual pass.

For a legged run, check contact, loading, push-off, swing/flight, and landing in a coherent order. Left and right limbs alternate; hips, knees, feet, torso lean, arm swing, and vertical body movement agree with the direction and gait. Grounded feet do not slide unintentionally; limbs do not pop, invert, merge, or gain joints. Flight is appropriate for the chosen gait, not mandatory for walking. A stylized run may exaggerate poses while retaining a readable cycle. For other forms, check their chosen propulsion and inertia instead of inventing legs.

For every frame check:

- Same character, facial locks, proportions, palette, accessories, line/pixel scale, and intended camera angle; no unexplained turning or feature flicker.
- Stable alignment and scale with only intentional motion; smooth pose progression and a coherent last-to-first loop, without teleporting or accidental duplicate holds.
- Sharp readable eyes, mouth, silhouette, and details at native size. Reject blurred or smeared frames, ghost limbs, compression damage, or inconsistent rendering. Do not use blur to hide a broken pose; intended effects must preserve the face and silhouette.
- Safe cell bounds, clean transparency, official row order and active frame counts.

Record `actions.<state>.qa` with `status` (`unreviewed`, `pass`, `fail`), `artifact`, and `issues`. Each issue names the affected frame(s), observable defect, and proposed correction. A script passing dimensions or transparency is only structural evidence. Mark visual QA `pass` only after actual inspection. Any failed or unreviewed row blocks completion.

## Review Choices And Immediate Changes

After generated previews and again after final row generation, show the actual animation and contact sheet, give a short QA result, and offer `保留`, `按建议修改`, `直接描述修改`, or `重做这个动作`. Suggest concrete fixes based on observed defects (for example, correct frame 4's planted foot, keep the left eye marking during the turn, or reduce torso bounce). Do not regenerate merely to populate a menu.

Accept edits immediately, including `左跑改成正面三分之二`, `右跑保持侧面`, `这个跑动重做`, or `脸不要变，脚步更自然`. Existing authorization to make the requested change is sufficient; do not restart the interview or ask for the same production approval again. If `重做` does not specify a new direction, retain the approved intent and correct observed issues; ask only if the target action is unclear.

Preserve the accepted version and unaffected rows. Update only the relevant action's angle, intent, beats and notes; clear its `preview_confirmed`, set QA to `unreviewed`, and record the request and previous artifact in `revision_history`. Regenerate the affected row through hatch-pet's supported workflow, reassemble a candidate atlas, rerun structural checks, and visually review the changed row plus its transitions and counterpart direction. A shared identity/base change requires review of all affected rows. Do not silently overwrite the accepted installed package before candidate review.

Show the new result with the same review choices. User acceptance does not waive failed QA, and QA passing does not imply user acceptance. Record `preview_confirmed=true` only for the current artifact after explicit acceptance; final delivery requires all current rows to pass QA and the user to accept the current action set. Allow a single acceptance of all displayed rows. On a failed row, attempt one targeted correction and re-review; if it still fails, show the evidence and propose next options instead of repeating generation indefinitely. Further retries follow the user's requested revision scope.

## Action Frame Image Delivery

Generate and show a separate frame strip for each action, alongside its animation preview. Director output QA exports lossless transparent `frames/<action>/frame-01.png` etc., a native-size `frames.png` strip, and `frames-4x.png` using nearest-neighbor enlargement. Use the original PNG frames for detail inspection; GIF palette conversion may reduce colors. Enlargement makes pixels easier to inspect but does not add detail or repair blurry source frames.

Require crisp source frames at the official 192x208 cell size, with readable facial details and consistent line/pixel treatment. If a frame fails, regenerate or correct its source through the supported row workflow and recheck the complete action. Do not label an upscaled blurry strip as high clarity. Show each action by name so the user can request `重做 jumping` or `只重做左跑`; preserve the other accepted rows and offer the replacement frame strip and animation for review.

## QA Is Required After Every Redo

Every redo or revision creates a new candidate artifact and invalidates the affected action's previous QA pass and user acceptance, even if its direction and beat sheet are unchanged. Set `qa.status=unreviewed` and `preview_confirmed=false` before generating the replacement. Never carry a previous artifact's QA pass into a new version.

For each replacement, rerun structural checks on the candidate atlas, inspect all active frames for clarity and identity consistency, and watch the complete action loop for motion logic and continuity. Compare directional movement against its counterpart and the production base. Record QA evidence against the current artifact; unresolved defects mean `fail`, and missing inspection means `unreviewed`.

Only a replacement that passes both structural and visual/motion QA and receives user acceptance may replace the accepted version. If QA fails, retain the accepted version and show the failed candidate's frame-specific issues and suggested corrections. Any further redo repeats this same QA cycle; there is no review exemption for retries or small edits.
