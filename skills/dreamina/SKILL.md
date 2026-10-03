---
name: dreamina
description: House rules for the `dreamina` (即梦) CLI — which video model tier to pick so a job does not sit in the slow queue, and the credit-spend line to report after every generation. Use BEFORE running any `dreamina` generator command (text2image, image2image, text2video, image2video, frames2video, multiframe2video, multimodal2video, image_upscale), when choosing a Seedance model, when a dreamina task is stuck at Queueing, or when the user says "用即梦/dreamina 生成视频/图片", "generate a video with dreamina", "seedance". Not for local image generation (zimage).
---

## Video queue: `_vip` = 快队列

Video generation has two queues, gated by model tier:

- `_vip` models (`seedance2.0_vip`, `seedance2.0fast_vip`) -> **快队列 / priority**:
  reach `queue_status: Generating` in ~1-2 min, finish in a few min.
- non-vip models (`seedance2.0`, `seedance2.0fast`, `seedance2.0mini`) -> **慢队列 / free**:
  can sit at `queue_status: Queueing` for 30-40+ min, sometimes effectively stuck.

Rule: any video that must land promptly -> ALWAYS use a `_vip` model. Non-vip only for
"don't care when it finishes". `_vip` also costs more and is the only tier reaching 1080p/4K.
There is NO CLI cancel -> a slow-queue task, once submitted, can't be aborted (only ignored).

## Report credits after every generation

Every generator call -> after it returns, report credit spend as a per-step line:

```
第N步 <cmd>: 消耗 <credit_count> credits, 余额 <total_credit>
```

`credit_count` -> from the task result JSON. Balance -> `dreamina user_credit`
(`total_credit`). Multiple calls in a turn -> one line each, plus a total-consumed
summary at the end.
