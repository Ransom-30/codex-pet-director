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

## Mandatory Canonical Character Consistency

The initially extracted and user-confirmed character establishes identity. The approved `confirmations.production_base` is its canonical animation reference at the official cell size; any necessary small-size simplification must be approved there once, not reinvented per action. Use that same base for every action and redo. Never use a newly generated action as a replacement identity reference without explicit approval of a base change.

Before row generation, record a concrete consistency contract in `appearance.visual_locks`: head-to-body and limb proportions, facial geometry, silhouette, hair shape, costume construction, accessory placement and anatomical side, colors, material/texture, highlight and shadow treatment, outline thickness or pixel scale, and recurring small details. Carry these locks into every action's `prompt_notes` and the hatch-pet identity/style notes. Preserve a stable camera scale and the character's underlying dimensions relative to the canonical cell; do not auto-fit each frame independently and thereby change its apparent size.

Pose, perspective, foreshortening and justified occlusion may change the projection. They must not change the underlying anatomy, material, costume, feature identity or rendering style. Any intentional squash/stretch must be specified in the approved action direction and return to the canonical proportions; do not silently use deformation to excuse model drift.

QA must compare every active frame of every action, including each redo, to the same production base and this contract. Check head/body ratio, limb lengths and thickness, face and hair geometry, outfit/accessory details, palette, texture grain, shading and edge treatment. Reject unexplained scale changes, material/style shifts, missing or invented details, and inconsistent simplification even when the animation otherwise moves smoothly. Record the affected frames and violated locks; regenerate affected rows and repeat QA. Preserve the accepted package while candidates fail review. If canonical details cannot remain readable at 192x208, revise and obtain approval for the production base, then review all affected actions rather than silently degrading individual frames.

## Mandatory Anatomy And Appendage Lock

Treat anatomy restrictions as one general first-image consistency rule, not a collection of special cases about hands. The initial user-confirmed extracted character defines the construction and proportions of every body part. Its approved production base carries that same design into animation; later action generation and redos change poses, not the character design. Lock head/body ratio, limb length and thickness, hand/foot or appendage shape, joint/attachment locations, and the presence or absence of parts. Apply the contract to all visible and subsequently revealed views; do not reinterpret a rounded end as a human hand, make a short arm longer, or invent unseen details without support from the approved design. When a hidden structure matters and cannot be inferred reliably, choose a pose that avoids inventing it or obtain clarification.


Before designing motion, identify the approved character's actual limb inventory and terminal shapes from the canonical reference: arms, legs, paws, wings, hands, fingers or their absence. Record these in `appearance.visual_locks`, including explicit prohibitions such as no hands, no fingers, rounded fabric arm ends, or no legs where applicable. Do not infer human anatomy from the character's humanoid outline.

An action name never authorizes new anatomy. For `waving`, a character without hands may raise or sway an existing arm, wing, rounded appendage, or its whole body. For a plush character with rounded fabric arm ends, preserve those rounded ends in every pose; never add a palm, thumb, fingers, finger divisions, a pointing hand, or a human fist. For a character with no arms, use an appropriate nod, tilt or other approved form-compatible greeting. Apply the same restriction to running, jumping, working, prop interaction and all redos. If a requested gesture requires absent anatomy, propose a compatible equivalent; changing the character's anatomy requires explicit user approval of a revised production base.

Inspect limb counts, attachment points and terminal silhouettes in every active frame, including raised-arm poses and perspective changes. Any invented hand, finger, extra limb, changed paw/wing construction or detached limb fails visual QA even when the texture, face and motion otherwise match. Pose or occlusion can explain visibility changes but cannot explain new anatomy. Name the offending frame and unsupported structure, correct the affected row, and repeat the full redo QA before accepting its replacement.

## General Motion Plausibility And Coordinated Poses

Design every action around the character's established construction, range of motion, balance and intended movement style. Stable proportions do not freeze the character: coordinate existing joints, head, torso and limbs to perform the action naturally. Use posture changes, a turn, a step, a bend or a smaller gesture when appropriate instead of distorting anatomy to reach a target or achieve a pose. For example, touching headwear may involve lowering the head toward an existing rounded arm end; this is one application of the general rule, not a required gesture or a special exception.

Plan a coherent sequence of preparation, movement, interaction/contact where relevant, release or recovery, and return. Preserve anatomical attachments and underlying limb dimensions throughout. Do not elongate an arm or leg, extend clothing as a hidden limb, shift a joint or attachment, detach a body part, invent anatomy, or teleport a prop to fake a result. Assess apparent length changes using plausible perspective and the approved style; explicitly approved squash/stretch may exaggerate motion but cannot excuse accidental drift.

When an action exceeds the character's reach, joint range or construction, choose a compatible variation. A character may adjust its own pose or move an object through a visible, plausible interaction; the target must not slide or snap into place without cause. If the requested outcome still cannot be performed with the locked anatomy, explain the limitation and suggest an alternative instead of silently deforming the character.

For every initial generation and redo, QA must inspect the full sequence and loop for plausible joint motion, stable limb lengths/thickness, connected head/torso movement, balance/support or the approved propulsion model, credible contact, and smooth recovery. Reject abnormal stretching, dislocation, unexplained penetration, snapping, impossible poses or invented anatomy. Record affected frames and the violated constraint, correct the affected action, and repeat structural and visual/motion QA before acceptance. Apply these checks to all actions and character forms, including greetings, locomotion, gestures, expressions with body motion, and prop interactions.

## Complete Alternating Gait Within The Fixed Frame Budget

The official `running-left` and `running-right` rows each have 8 active frames. For an approved alternating biped run, use those 8 frames for a complete two-sided gait cycle rather than several repeated poses with a single leg-swap frame. A default planning template allocates 4 sequential phase samples to each leg-led half-cycle: contact/loading, support/push-off, swing/flight as appropriate to the gait, and approach to the opposite contact. The second half reverses the leg roles and connects smoothly back to frame 1. This is a production planning template, not a universal physical timing rule; adapt phase durations and supported poses to the character and reference while keeping both sides fully represented.

Write an explicit 8-frame beat sheet identifying anatomical left/right leg roles, support/contact, swing and torso response. Both alternating halves must have multiple evolving poses, not one isolated swapped pose. Do not satisfy the frame budget with duplicate images or change only the head while the legs remain static. Do not equate 4 phase samples with 4 frames of one grounded foot, force flight for walking, or force alternating legs on hopping, floating, sliding or legless characters; evaluate those approved locomotion types with a complete cycle of their own.

QA must inspect frames 1 through 8 and the 8-to-1 transition, track each anatomical leg across the complete loop, and verify that both leg-led halves have a readable progression and comparable motion coverage consistent with the intended gait. Reject a lone swapped-leg frame, repeated dominant stance, foot-role popping, unsupported asymmetry, or duplicated poses that hide a missing half-cycle. Symmetry does not require mirrored images: perspective, occlusion and approved asymmetrical construction may differ while the gait remains coherent. Every regenerated row must repeat this check. The 6-frame official `running` working state is distinct from directional locomotion and does not impose this biped gait template.

## Arm And Leg Coordination In Ordinary Biped Runs

For ordinary alternating biped running with freely swinging arms, plan contralateral coordination: as the anatomical left leg swings forward, the right arm swings forward, and vice versa. Arm reversal must follow the gait continuously, not change sides abruptly at one frame. Track anatomical sides rather than screen-left/screen-right, especially in angled views and turns. Match swing range to the canonical short or long appendages; never lengthen an arm to make its swing visible or add hands/fingers.

Include arm direction and phase alongside leg roles in the 8-frame beat sheet. During QA of every generated and redone row, inspect both arms and legs across both half-cycles and the loop seam. Reject unintended same-side arm/leg forward swing (顺拐), phase popping, static or duplicated swings that conceal the error, or arm motion disconnected from torso and gait. A neutral crossover pose alone is not evidence of a coordination error; inspect the temporal sequence.

If the approved action explicitly holds a prop, keeps arms fixed, uses nonhuman locomotion, or intentionally depicts a different stylized gait, evaluate that specific performance instead of forcing free arm swing. Do not use an unrequested exception to excuse accidental 顺拐 in an ordinary run.

## Shared And Action-Specific QA

Use two layers of review for every action and every redo. First apply the shared contract: canonical anatomy/proportions/materials/details, native-size clarity, stable alignment and scale, plausible joint connections, intentional pose progression, and coherent timing. Then apply only the motion checks relevant to the approved performance and character form. Do not force humanoid support, gravity-driven movement or literal limbs on an approved floating or nonhuman character.

Inspect lossless frame images, a slow animation preview, and a normal-speed preview. Frames reveal structural defects, slow playback reveals phase/contact discontinuities, and normal playback reveals rhythm and readability. If a preview is unavailable, record the limitation rather than claiming it was reviewed. Director row GIFs use a fixed diagnostic duration and do not establish actual app playback speed; use hatch-pet runtime timing or an observed runtime preview when judging normal-speed behavior.

| Performance | Relevant checks |
| --- | --- |
| Ground locomotion | Planted feet do not unintentionally slip or penetrate the support surface; lift/landing and weight transfer are continuous. Torso lean and bob agree with the gait. When actual displacement is shown, speed and step cadence should agree. Do not judge a stationary diagnostic loop as sliding merely because it has no world translation. |
| Jumping | Preparation, push-off, ascent/airborne pose, descent, landing and recovery form a coherent sequence where the approved action depicts a full jump. Landing has a plausible settling response for the character's construction; no teleporting height changes or forced flight on non-jumping performances. |
| Greeting, nodding, turning | Existing joints and head/body attachments remain connected; motion reverses or settles smoothly. Perspective and occlusion preserve face identity, anatomical sides and accessory locations. |
| Touching, carrying, releasing props | Approach precedes contact; contact and object movement have an observable cause; held objects follow their attachment; separation follows release. No penetration, remote grasping, or unexplained prop snapping. Preserve the character's actual grasp/appendage capability. |
| Sitting, crouching, leaning | Coordinate torso, hips and available limbs with plausible support and balance; preserve underlying dimensions instead of shortening legs or stretching the torso. |
| Expressions and blinks | Expression changes preserve facial layout and identity. Blinks must not change eye placement, hair, markings or face proportions accidentally; deliberate eye/mouth shape changes follow the approved acting. |
| Breathing, idle, waiting | Subtle intentional movement is readable without whole-body jitter, flickering contours, accidental pulsing scale or randomly drifting details. |
| Failure, surprise, exaggerated acting | Exaggeration follows the approved beats and style. Deliberate deformation must be approved and recover coherently; accidental dislocation, elongation or identity drift is never excused as acting. |

Across relevant actions, inspect joints for abrupt inversion, detached connections or changed attachment locations. Check occluded appendages reappear from the correct anatomical place; visibility may change naturally without inventing structure. Clothing and accessories follow their established attachments (sleeves to arms, cap to head); secondary hair/fabric motion may lag the primary motion when appropriate to the locked material, without random floating, altered construction or texture shifts. Keep these checks proportional to what is visible at the official cell size.

## Transitions Between Actions

In addition to each row's loop seam, review the state transitions supported by the existing runtime, especially idle into motion/gesture and return where applicable. Compare alignment, character scale, facial identity and detail treatment across row endpoints. Reject unintended position/scale jumps or identity/material changes. An intentional state-specific pose change may occur, but should remain visually coherent; do not demand every action start in the same pose or add unsupported transition frames/states to the official format.

Use an available runtime preview to assess actual switching behavior. If only rows can be inspected, review their boundary poses as partial evidence and explicitly report runtime transitions as unverified. A change to shared alignment, base design or timing requires re-review of all affected rows and transitions, including after a targeted redo.

## How To Generate The Eight-Frame Alternating Run

Before requesting a directional run row, write a numbered eight-frame plan tied to anatomical sides. Do not prompt only "4+4 frames" or generate one pose and mirror/duplicate it to fill the row. Use the approved production base and locks as the canonical reference in the supported hatch-pet workflow. Supply the full cycle plan to the row generator; the phases below are a default stylized biped run example, not immutable physical timing.

| Frame | Leg-led phase | Arm coordination and body response |
| --- | --- | --- |
| 1 | Anatomical left foot reaches forward and contacts the support; right leg trails. | Right arm forward, left arm back; torso enters loading. |
| 2 | Left support loads then progresses toward push-off; right leg recovers forward. | Arms progress smoothly toward crossover; body compresses then begins rising. |
| 3 | Left push-off transitions to the intended swing/flight phase; right leg advances. | Arms cross continuously toward left-arm-forward; no new limb shapes. |
| 4 | Right foot approaches the next contact; left leg trails/recovering. | Left arm increasingly forward, right arm back; body approaches loading. |
| 5 | Anatomical right foot contacts; left leg trails. | Left arm forward, right arm back; role reversal of frame 1. |
| 6 | Right support loads then progresses toward push-off; left leg recovers forward. | Arms progress toward crossover; body response matches frame 2's role-reversed phase. |
| 7 | Right push-off transitions to the intended swing/flight phase; left leg advances. | Arms cross toward right-arm-forward; preserve canonical proportions. |
| 8 | Left foot approaches the next contact, completing the loop into frame 1. | Right arm increasingly forward, left arm back; smooth contact/torso continuation into frame 1. |

Use perspective and occlusion appropriate to each row's independently approved angle. Label anatomical sides consistently across all frames; screen-left/right is not a substitute. Adjust the template to the actual gait/reference, especially short-limbed plush construction, without forcing unreachable strides, flight or humanoid joints. Distinguish frame 4 (approach) from frame 5 (contact) and frame 8 (approach) from frame 1 (contact), rather than duplicating boundary poses.

Include these row-prompt constraints: exactly 8 active sequential frames in official order; one complete alternating cycle; distinct evolving contact/loading/push-off/recovery samples on both sides; opposite free arm/leg swing; stable camera and scale; locked anatomy/materials/face; no duplicate padding, single-frame leg swaps, blur or stretched limbs. Explicitly describe the approved stride amplitude and view angle. Do not add extra official frames, run independent unconstrained character redesigns per cell, or introduce a custom generation pipeline outside hatch-pet.

After generation, compare the actual frames with the numbered plan. Record observed leg support/swing and arm direction per frame, marking obscured evidence as uncertain rather than inventing it. Inspect temporal progression and the 8-to-1 seam; an eight-cell output is not proof that the plan was followed. A missing half-cycle, unexplained phase reversal, same-side swing or duplicated padding fails QA. Diagnose the offending frames, revise the affected row's prompt/beat sheet, regenerate through the supported workflow, and repeat the complete row QA. If detailed timing cannot fit the fixed budget, simplify the gait or stride while retaining a complete readable cycle.
