# Case 2

- **Bug:** Commented out `StandardScaler` so features are not scaled.
- **Observed:** No crash. Saved run: test accuracy ~0.578, test loss ~0.684 vs baseline ~0.708, ~0.561.
- **Initial reflection (weak):** Accuracy is lower maybe because random seed changed.
- **GenAI:** Bad. Guidance: What changed in preprocessing besides randomness? Are your feature scales comparable now? How can unscaled ranges affect gradient-based optimization?
- **New reflection:** I removed StandardScaler, so features stayed on their raw scales. With no code error, test accuracy was about 0.578 and loss about 0.684 vs about 0.708 and 0.561 with scaling; the drop matches worse-conditioned inputs, not a different seed.
- **Fix:** Restore `StandardScaler().fit_transform(X)`.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
