# Case 9

- **Bug:** Decision threshold 0.9 instead of 0.5 for train-metric predictions and test predictions.
- **Observed:** No crash. Test accuracy ~0.649; diabetes recall 0; confusion matrix [[100,0],[54,0]].
- **Initial reflection (weak):** The model became bad at diabetes prediction for unknown reasons.
- **GenAI:** Bad. Guidance: Is the issue in training weights or in decision thresholding? How does raising threshold from 0.5 to 0.9 change class-1 recall?
- **New reflection:** 0.9 is so high almost nothing passed as positive. The saved run shows diabetes recall 0 and confusion matrix [[100,0],[54,0]] (all predicted negative); test accuracy about 0.649; that was thresholding, not a failed training loop.
- **Fix:** Restore threshold 0.5 (or pick a threshold from validation).

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
