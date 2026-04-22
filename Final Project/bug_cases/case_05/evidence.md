# Case 5

- **Bug:** `nn.Linear(10, 16)` instead of `nn.Linear(8, 16)` in first layer.
- **Observed:** `RuntimeError: mat1 and mat2 shapes cannot be multiplied (614x8 and 10x16)` on first forward pass.
- **Initial reflection (weak):** The layer is probably too big so training fails.
- **GenAI:** Bad. Guidance: How many input features are actually fed into the model? What matrix dimensions are multiplied in the first linear layer?
- **New reflection:** There are 8 features per row but fc1 expected 10. The first forward pass crashed with mat1 and mat2 cannot be multiplied (614x8 and 10x16); the width was wrong, not the layer being too big.
- **Fix:** Restore `nn.Linear(8, 16)`.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
