# Case 8

- **Bug:** `optimizer.zero_grad()` commented out in the training loop.
- **Observed:** No crash. Saved run: test accuracy 0.7078 (same as baseline) but confusion matrix [[98,2],[43,11]] vs baseline [[91,9],[36,18]].
- **Initial reflection (weak):** Optimizer is weak so results are weird.
- **GenAI:** Bad. Guidance: Are gradients reset each step? If not, what happens to accumulated gradients across epochs?
- **New reflection:** With zero_grad removed, gradients accumulate each step. The run still finished; headline test accuracy matched baseline at 0.7078 but the confusion matrix differed ([[98,2],[43,11]] vs [[91,9],[36,18]]), so training was affected even when accuracy looked the same.
- **Fix:** Uncomment `optimizer.zero_grad()` each iteration.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
