# Case 7

- **Bug:** `CrossEntropyLoss()` instead of `BCELoss()` without changing outputs or label dtype/shape.
- **Observed:** No crash. Training loss about -0, test accuracy ~0.35, confusion matrix `[[0,100],[0,54]]` (degenerate).
- **Initial reflection (weak):** CrossEntropy just performs worse than BCE here.
- **GenAI:** Bad. Guidance: Does CrossEntropyLoss expect the same output/target format as BCE? What output shape and target type are you providing now?
- **New reflection:** This build uses one sigmoid output and float 0/1 labels for BCE. CrossEntropy needs class logits and long class indices. The run showed loss about -0, test accuracy about 0.35, confusion matrix [[0,100],[0,54]] predicting only class 1; that fits target-format mismatch, not CrossEntropy simply being weaker.
- **Fix:** Restore `BCELoss` with current architecture, or redesign outputs and labels for CrossEntropy.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
