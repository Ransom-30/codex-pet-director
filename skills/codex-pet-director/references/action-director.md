# Action Director

Use this guide when the character form, personality, style, and production base are settled enough to design motion.

The goal is not to ask nine technical questions first. The goal is to let the user express the character moments they care about, then fill the fixed Codex action slots with a coherent performance plan.

## Entry Line

Say:

```text
接下来我会设计它的 9 个官方动作。
你不用从零想完整动画。先告诉我：这个角色有没有哪几个动作你特别想看到？
比如平时、失败、等待、查看结果、鼠标碰到、打招呼、移动、工作中，它应该表现出什么性格？
```

If the user gives specific requests, capture them first. Do not overwrite them with generic presets.

If the user says they do not know, say:

```text
没关系，我会根据它的形态、性格和风格先推荐一套动作，你再挑不喜欢的地方改。
```

## Capture User Intent

Translate user language into action intent:

| User says | Record as |
| --- | --- |
| 平时抱臂、很拽 | `idle.special_request` |
| 失败时要生气，不要沮丧 | `failed.special_request` and avoid sad acting |
| 等我回复时催我一下 | `waiting.special_request` |
| 有结果时像审判别人 | `review.special_request` |
| 鼠标碰到时警觉 | `jumping.special_request` |
| 不要热情挥手，冷淡点头 | `waving.special_request` |
| 移动时像漂浮，不要跑步 | `running-right`, `running-left`, `running` special requests |

Most users will only specify 2-4 important moments. Fill the rest yourself.

## Complete The 9 Slots

After collecting special requests, output:

```text
你刚刚明确了：
- idle: ...
- failed: ...
- review: ...

剩下的动作我会按它的性格补齐。
```

Then provide a full action card:

```text
idle:
running-right:
running-left:
waving:
jumping:
failed:
waiting:
running:
review:
```

For every action, mark the source internally:

- `user`: the user explicitly requested it.
- `mixed`: the user gave a direction and the director filled the beats.
- `recommended`: the director filled it from character/personality/form.

## Recommendation Rules

Build recommendations from:

- form: full-body, half-body, head-only, screen-face, floating object, anthropomorphic object
- personality: calm, proud, angry, funny, mysterious, careful, warm, strict
- role: assistant, partner, supervisor, trickster, teacher, tester, judge
- style: cute, cyber, pixel, chibi, magic, office, funny, dark

Do not use the same generic actions for every pet. Make the action attitude match the character.

Examples:

- Proud warrior: crossed arms, short nod, angry failed reaction, judging review.
- Gentle helper: soft wave, patient waiting, worried failed reaction, pleased review.
- Trickster: cheeky idle, fake-innocent failed reaction, teasing waiting.
- Screen-face helper: eye blink, screen flicker, tilt, face expression, tiny bounce.

## Form Adaptation

Never force literal limbs when the form does not support them.

- Full-body: run, hop, jump, wave, stomp, crouch, turn.
- Half-body: shoulder bob, head tilt, hand gesture, expression change, hair/prop motion.
- Head-only: bounce, drift, blink, eyebrow change, face squash, hair motion.
- Screen-face: screen flicker, eye shape change, small tilt, loading pulse.
- Floating object: bob, tilt, rotate, tiny jet, attached prop movement.
- Object mascot: wobble, slide, lid/handle motion, face expression.

## Beat Sheets

Every final action should get a short beat sheet. Use simple words, one beat per frame when possible.

Examples:

`idle` 6 frames:

```text
1 stable pose, 2 slight inhale, 3 blink, 4 hair/prop moves, 5 exhale, 6 returns to loop
```

`failed` 8 frames:

```text
1 freeze, 2 eyes tighten, 3 body drops, 4 angry puff attached to body, 5 clenched pose, 6 holds, 7 recovers, 8 settles
```

`review` 6 frames:

```text
1 leans in, 2 eyes narrow, 3 scans, 4 judges, 5 nods or frowns, 6 returns to focus
```

## Preview Policy

Group requested actions into batches of 2–3 for generation and a single shared review. Choose the first batch from user priorities, or related actions such as idle and both movement directions. Do not require five preliminary rows or separate key-pose approval. Final generated actions are shown for review using `action-review.md`. Record preview flags for the actual workflow; reuse existing user approval rather than asking again.

## User Revision Language

Accept short natural edits:

- `全部确认`
- `改 failed`
- `waving 改成点头`
- `running-left 不要镜像`
- `waiting 不要催我，改成安静等`
- `失败不要难过，要生气`

Update only the requested actions and show the revised action card.

## Generated Action Review

Use [action-review.md](action-review.md) for independent left/right angles, motion and facial consistency checks, and review choices after generation. Action-card approval approves intent only; generated rows still require visual QA and acceptance.

## Production Motion Plan

Use [motion-planning.md](motion-planning.md) for a concise action description or beat sheet. Detailed per-frame plans are optional; do not make them a generation prerequisite.
