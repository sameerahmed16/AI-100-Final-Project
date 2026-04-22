# Case 3

- **Bug:** Removed `stratify=y` from `train_test_split`.
- **Observed:** No crash. Test support 99/55 vs baseline 100/54; test accuracy ~0.766 vs baseline ~0.7078 (can go up or down; split is not comparable).
- **Initial reflection (weak):** Model got different accuracy because neural networks are unstable.
- **GenAI:** Bad. Guidance: Did you compare class ratios in train/test before and after the split change? Could sampling differences explain metric shifts without changing model architecture?
- **New reflection:** Removing stratify changed test-set class counts (99 vs 100 negatives, 55 vs 54 positives in my saved run). Test accuracy actually went up to about 0.77 vs about 0.71 for the stratified baseline, so the point is the split is not comparable to baseline, not that accuracy always drops.
- **Fix:** Restore `stratify=y`.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
