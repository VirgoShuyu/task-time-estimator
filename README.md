# task-time-estimator

A [QoderWork](https://qoder.com) skill that estimates how long a task will take before starting it.

## What it does

Before executing any multi-step task, this skill:

1. **Decomposes** the task into individual steps
2. **Estimates** each step using a baseline cost table (e.g., web search ~30s, file edit ~15s, doc generation ~2min)
3. **Applies** a 1.5x buffer for uncertainty
4. **Outputs** a natural one-liner like: "⏱ About 5 minutes, grab a coffee"

It also:
- **Auto-injects** the estimation rules into your `AGENTS.md` on first use, so every future conversation gets time estimates automatically
- **Logs actual duration** after each task completes, building a feedback loop that refines the baseline table over time

## Install

### QoderWork

```bash
git clone https://github.com/VirgoShuyu/task-time-estimator.git ~/.qoderwork/skills/task-time-estimator
```

### Claude Code

```bash
git clone https://github.com/VirgoShuyu/task-time-estimator.git ~/.claude/skills/task-time-estimator
```

## How it works

| Step type | Baseline |
|-----------|----------|
| Web search | ~30s |
| File read | ~10s |
| MCP tool call | ~15s |
| File edit | ~15s |
| Doc generation | ~2min |
| Code writing | ~2min |
| Subagent | ~1-2min |
| Browser automation | ~2min/page |
| Data analysis | ~3min/round |

Total = sum of steps × 1.5 buffer

## Feedback loop

After each multi-step task, the skill records:
```
[耗时记录] 预估: 5min | 实际: 3min | 类型: GitHub发布 | 步骤: 4步
```

After 20+ entries, it statistically calibrates the baseline table for your actual environment.

## License

MIT
