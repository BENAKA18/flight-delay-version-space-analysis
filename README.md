# Find-S & Candidate Elimination: Version Space Analysis

[![Python 3.7+](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)
[![Colab](https://img.shields.io/badge/Google-Colab-orange.svg)](https://colab.research.google.com/)

## Overview

This project implements two fundamental concept learning algorithms in Machine Learning:

- **Find-S Algorithm** - Finds the most specific hypothesis consistent with all positive examples
- **Candidate Elimination Algorithm** - Maintains both specific (S) and general (G) boundaries to represent the entire version space

The implementation demonstrates **5 scenarios** where the version space becomes impossible (empty) using a unique synthetic dataset: **Flight Delay Prediction**.

## Algorithms

### Find-S Algorithm

```
Input: Training examples (positive and negative)
Output: Most specific hypothesis S

Steps:
1. Initialize S = [∅, ∅, ..., ∅]
2. For each positive example:
     For each attribute i:
       if S[i] = ∅ → set to example value
       else if S[i] ≠ example value → set to '?'
3. Ignore negative examples
4. Return S
```

### Candidate Elimination Algorithm

```
Input: Training examples (positive and negative)
Output: S (specific boundary) and G (general boundary)

Steps:
1. Initialize S = [∅, ∅, ..., ∅]
          G = [?, ?, ..., ?]
2. For each positive example:
     - Generalize S to cover the example
     - Remove from G any hypothesis not covering the example
3. For each negative example:
     - Specialize G to exclude the example
     - Keep only hypotheses more general than S
4. Version Space = { h | S ≤ h ≤ G }
5. If G empty or S covers negative → Version Space EMPTY
```

## Dataset

### Flight Delay Prediction

| Attribute | Possible Values |
|-----------|-----------------|
| Airline | Delta, United, American, Southwest |
| TimeOfDay | Morning, Afternoon, Evening, Night |
| DayOfWeek | Weekday, Weekend |
| Season | Summer, Winter, Spring, Fall |
| AirportSize | Large, Medium, Small |
| Weather | Clear, Rain, Snow, Storm |
| PreviousDelay | Yes, No |
| Congestion | High, Medium, Low |

**Target:** Delayed (Positive) / On Time (Negative)

## 5 Situations Where Version Space Becomes Empty

| # | Situation | Root Cause |
|---|-----------|------------|
| 1 | Identical examples with different labels | Contradiction/Noise in data |
| 2 | Positive more specific than negative | Hypothesis space too weak |
| 3 | XOR pattern | Needs disjunction (OR) |
| 4 | Missing crucial attribute | Incomplete representation |
| 5 | Sequential contradiction | Inconsistent algorithm updates |

## Usage

### Google Colab (Recommended)

1. Go to [Google Colab](https://colab.research.google.com/)
2. Click **File → Upload Notebook**
3. Upload `flight_delay_version_space.ipynb`
4. Click **Runtime → Run all**

### Local Jupyter Notebook

```bash
jupyter notebook flight_delay_version_space.ipynb
```

## Output Format

Each situation displays output in the following format:

```
======================================================================
SITUATION X: [Situation Name]
======================================================================

[INPUT]
  E1: {attribute: value} → Positive
  E2: {attribute: value} → Negative

[FIND-S]
  Final S: {attribute: value}

[CANDIDATE ELIMINATION]

  After E1: Positive
    S = {attribute: value}
    G = [{attribute: value}]

  After E2: Negative
    S = {attribute: value}
    G = []
    >>> VERSION SPACE EMPTY <<<

[RESULT] Version Space: EMPTY

[WHY] Explanation of why version space is impossible
```

## Results

| Situation | Version Space |
|-----------|---------------|
| 1: Identical different labels | ❌ EMPTY |
| 2: Positive ⊏ Negative | ❌ EMPTY |
| 3: XOR pattern | ❌ EMPTY |
| 4: Missing attribute | ❌ EMPTY |
| 5: Sequential contradiction | ❌ EMPTY |

**All 5 situations result in EMPTY version space.**

## Project Structure

```
flight-delay-version-space-analysis/
│
├── README.md                           # Documentation
└── flight_delay_version_space.ipynb    # Main notebook
```

## Technologies Used

- Python 3.7+
- Google Colab / Jupyter Notebook

## License

MIT License - Free for educational use.

---

