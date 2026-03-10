# Beacon: Protect-Then-Select Attention Architecture
(MG-OS + GD-Attention Demo)

<p align="center">
  <img src="protect_then_select_architecture.png" width="720" alt="Beacon protect-then-select attention architecture">
</p>

**Related resources**

Paper (preprint)  
MG-OS: [https://zenodo.org/records/17712891](https://zenodo.org/records/17712891)  
GD-Attention: [https://zenodo.org/records/16757311  ](https://zenodo.org/records/16757311  )

Project page  
[https://www.ghostdriftresearch.com/](https://www.ghostdriftresearch.com/)

Repository  
[https://github.com/GhostDriftTheory/beacon](https://github.com/GhostDriftTheory/beacon)


**Minimal architecture demo of:**

- **Transformer-style softmax attention**
- **MG-OS conditional barrier layer**
- **GD-Attention-style single-candidate selection**

This repository visualizes a compact architectural contrast:

**Softmax mixes.**  
**MG-OS + GD-Attention protects at-risk minority-important signals and then selects.**

Because Beacon intervenes in the protection and final selection of semantic candidates, it should be treated as a high-sensitivity architecture requiring careful evaluation and interpretation.

---

## Core architecture path

```text
Transformer-like attention logits
↓
MG-OS conditional barrier
↓
GD-style single selection
```

This demo is designed to make that path visible in a small, reproducible form.

---

## What this updated demo shows

The app compares two routes on the same toy task.

### 1. Baseline: softmax attention

- compute attention logits
- apply softmax
- mix candidate values
- produce an output distribution

### 2. Proposed: MG-OS + GD-Attention

- compute attention logits
- detect whether a minority-important candidate is at risk of premature collapse
- activate an **MG-OS-style barrier** only in those risky cases
- preserve the candidate above a protective floor or near-contention region
- apply **GD-style single-candidate selection**
- produce an output from the selected candidate

---

## Main visible outputs

This app focuses on the following architecture-level differences:

- **minority survival**
- **minority recall**
- **minority top-2 retention**
- **collapse avoidance**
- **rescue rate**
- **false rescue rate**
- **barrier activation rate**
- **Gamma proxy shift**

The point is not only whether the final prediction changes, but **how the internal competition changes before selection**.

---

## Representative case view

The app shows one representative case in detail.

Rather than displaying an arbitrary minority example, it preferentially displays a **representative rescue case**:

- a case where softmax fails
- but MG-OS + GD-Attention succeeds

If no such case exists under the current setting, the app falls back to:

- the largest gamma-gain minority case, or
- the hardest raw-minority case

For that case, the app visualizes:

- query and candidate-key geometry
- raw attention logits vs barriered logits
- softmax weights vs protected weights
- softmax mixed output vs GD-style selected output
- minority rank change
- Gamma change
- barrier boost size

This is meant to make the **protect-then-select** mechanism directly observable.

---

## Batch evaluation view

The app also evaluates the architecture over many samples.

It reports:

- accuracy
- balanced accuracy
- minority survival
- minority recall
- minority top-2 retention
- collapse rate on minority cases
- rescue rate
- false rescue rate
- barrier activation rate
- mean Gamma delta

These metrics are intended to show not only whether the proposed route helps minority-important cases, but also whether it does so **without blindly biasing every sample**.

---

## Why the conditional barrier matters

This demo does **not** implement the barrier as a permanent minority bias.

Instead, the barrier is intended to activate only when the minority-important candidate is:

- near contention,
- under a protective floor,
- or in an ambiguous competitive state.

This makes the demo closer to an **architecture intervention** than to a fixed class preference.

---

## Ethical significance and careful handling

Beacon should not be treated as a mere performance-oriented attention variant.

The core issue in this architecture is not only how strongly candidates are weighted, but which candidates are protected, which candidates are allowed to collapse, and which candidate is ultimately granted representational priority. In other words, Beacon intervenes not only in numerical mixing, but in the structure of semantic competition itself.

This matters because the architecture explicitly introduces a protect-then-select path:

- a candidate judged to be at risk may be preserved by the MG-OS barrier,
- and a final representative may then be determined by GD-Attention-style selection.

Once this kind of intervention is introduced, the architecture can no longer be understood only through surface-level metrics such as accuracy gains or efficiency changes. What must also be examined is:

- which candidates are protected,
- under what conditions barrier activation occurs,
- when rescue is appropriate,
- when false rescue is introduced,
- and how final selection changes the distribution of representational priority.

For that reason, Beacon belongs to a technically and ethically sensitive category. It touches not only model behavior, but also broader questions of:

- explanation,
- accountability,
- safety boundary design,
- minority-important signal preservation,
- and the responsible interpretation of internal selection dynamics.

This does **not** mean that the repository claims to solve AI ethics, nor does it claim consciousness, agency, or moral status for current AI systems. The point is narrower and more concrete:

**if an architecture explicitly intervenes in which semantic candidates survive and which one is selected, then that architecture should be evaluated and communicated with unusual care.**

In practical terms, Beacon should therefore not be read as a simple "accuracy trick" or as a generic architectural tweak. Its significance lies in making internal selection structure more visible and more deliberate. That visibility is valuable, but it also creates design responsibility.

Accordingly, this repository is presented as a compact research demo for careful inspection of:

- rescue behavior,
- collapse avoidance,
- barrier activation,
- Gamma proxy changes,
- and the structural difference between mix-first and protect-then-select paths.

It is **not** presented as a ready-made high-stakes deployment recipe. Any future use in socially sensitive or safety-critical contexts would require case-specific evaluation, interpretability analysis, failure-mode study, and explicit responsibility design.

---

## Presets included

The app includes three initial presets:

- **Rescue-first**
- **Balanced**
- **Mild stress**

These presets are there so the architectural contrast is visible quickly, especially in the rescue-oriented regime.

---

## Repository structure

- `app.py` — Streamlit app
- `requirements.txt` — minimal dependencies

---

## Run locally

```bash
pip install -r requirements.txt
streamlit run app.py
```

---

## Interpretation

This is a **compact architecture demo**, not a production model.

Its purpose is to make the following structural claim visible:

- standard softmax attention primarily **mixes**
- MG-OS introduces a **conditional protective barrier**
- GD-Attention then **selects** instead of blending everything away

The intended contribution of the demo is therefore not large-scale benchmark performance, but a visible contrast between:

- **mix-first architectures**
- and
- **protect-then-select architectures**

---

## Scope

This repository does **not** include:

- a full transformer implementation
- a full MoE implementation
- LLM training
- real-world deployment claims
- large-scale benchmark claims

It is a compact visualization of an architecture idea.

