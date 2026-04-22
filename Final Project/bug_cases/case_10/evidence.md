# Case 10

- **Bug:** `model.eval()` commented out before test evaluation (dropout still active in training mode).
- **Observed:** No crash. Saved run: test accuracy 0.6948, test loss 0.5739 vs baseline ~0.7078, ~0.5609.
- **Initial reflection (weak):** Evaluation changed because PyTorch is nondeterministic.
- **GenAI:** Bad. Guidance: During evaluation, is the model in train mode or eval mode? What does dropout do in each mode?
- **New reflection:** I left the model in train mode during the test pass, so dropout was still on. The saved run had test accuracy 0.6948 vs 0.7078 baseline and slightly higher test loss (0.5739 vs 0.5609); that matches eval mode and dropout, not generic nondeterminism.
- **Fix:** Call `model.eval()` before evaluating on the test set.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
