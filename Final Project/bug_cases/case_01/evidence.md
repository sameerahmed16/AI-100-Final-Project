# Case 1

- **Bug:** Wrong label column name (`Outcomes` instead of `Outcome`).
- **Observed:** `KeyError: 'Outcomes'` at class distribution / column access before training.
- **Initial reflection (weak):** The code is broken because pandas is not working.
- **GenAI:** Bad. Guidance: Which exact line throws the first error? What column names exist in the dataframe at that moment? Is this a library failure or a schema/key mismatch introduced by your change?
- **New reflection:** I changed the label to Outcomes but the CSV column is still Outcome. The run failed with KeyError: 'Outcomes' at the class-distribution line before any training, so it was a wrong column name, not pandas being broken.
- **Fix:** Restore `Outcome` everywhere for labels and drops.

Artifacts: `buggy_train.py`, `fixed_train.py`, `run_bug_output.txt`, `run_fixed_output.txt`, `genai_prompt_and_response.txt`.
