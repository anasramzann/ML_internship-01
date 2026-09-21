# Prompt Engineering Ladder — FlyRank Search Intelligence

This document tracks the iterative improvement of an AI prompt for analyzing low-engagement search content.

---

## Baseline Prompt (Run 0)

### Prompt
> "Write a python script to find bad pages in my website data."

### Output Excerpt
```python
import pandas as pd
df = pd.read_csv('content.csv')
bad_pages = df[df['traffic'] < df['traffic'].mean()]
print(bad_pages)
