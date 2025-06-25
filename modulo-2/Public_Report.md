### Public Report — Module 2

**Public Report: Homomorphic Encryption in Neural Networks**

**Authors**:
- Bianca Lima
- Luiz Alencar
- Marcos Silva

**Supervisor**: Cristina Gramani

**Institution**: Inteli - Instituto de Tecnologia e Liderança

---

#### Table of Contents

1. [Introduction](#introduction)
2. [Module 2 Scope and Goals](#module-2-scope-and-goals)
3. [Sprint-by-Sprint Summary](#sprint-by-sprint-summary)
4. [Methodological Insights and Reorientation](#methodological-insights-and-reorientation)
5. [Discussion and Lessons Learned](#discussion-and-lessons-learned)
6. [Conclusion](#conclusion)

---

<a id="introduction"></a>
### 1. Introduction

Module 2 focused on critically reassessing the initial architecture developed in Module 1, refining the article draft, updating the codebase, and preparing the system for future deployment. Most importantly, it addressed a crucial limitation discovered when testing real homomorphic encryption via Microsoft SEAL, which led to a methodological pivot to maintain feasibility while preserving the original research intent.

---

<a id="module-2-scope-and-goals"></a>
### 2. Module 2 Scope and Goals

| Goal                                                  | Status       | Notes                                                                                                            |
| ----------------------------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------- |
| Identify and resolve architectural flaws              | ✅            | Re-evaluated encryption pipeline; replaced overly noisy operations; redesigned activation pipeline.              |
| Refactor code for clarity, reproducibility, and speed | ✅            | Split prototype into modular PyTorch + backend;                                    |
| Deliver final reviewed draft + public report          | ✅            | See Sprint 5 deliverables.                                                                                       |
| Submit to conference                                  | ❌ (deferred) | Deferred to next module pending additional experiments.                                                          |

---

<a id="sprint-by-sprint-summary"></a>
### 3. Sprint-by-Sprint Summary

| Sprint                                 | Main Activities                                                                                             | Deliverables                                     |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| **S1 – Planning**                      | Defined Module 2 milestones.                                                     | Module 2 project plan.                           |
| **S2 – Article Review**                | Discovered an architecture issue | Architecture issue log. |
| **S3 – Code Refactor v1**              | Updated tokenization, applied randomized tensor simulation, and improved structure. | `v0.2` codebase.             |
| **S4 – Code Refactor v2 & Benchmarks** | Implemented evaluation metrics, training curves, sentiment demo, and ONNX model export.                       | `v0.3` codebase; benchmark notebook.             |
| **S5 – Final Draft & Report**          | Integrated new results, regenerated plots, final proofreading, compiled this public report.                 | Paper draft vFinal; Public Report (M2).          |

---

<a id="methodological-insights-and-reorientation"></a>
### 4. Methodological Insights and Reorientation

While exploring the integration of Microsoft SEAL for homomorphic encryption (CKKS scheme), we encountered a significant technical barrier:
Encrypted input tokens generated using SEAL are non-deterministic and irreversible, due to the combination of Fourier Transform techniques and RLWE (Ring Learning With Errors). Each encryption of the same token results in a different ciphertext, making it impossible to recover or trace the original input even within inference flows.
This limitation broke compatibility with traditional NLP workflows, particularly in transformer models that expect repeatable token IDs for embedding lookup.
As a solution, we introduced a simulation mechanism: a vocab_randomized_tensor that consistently remaps token IDs to randomized equivalents. While not using actual encryption, this approach emulates obfuscation and allows the model to operate in a pseudo-encrypted setting—useful for research on robustness, noise, and privacy preservation patterns.

---

<a id="discussion-and-lessons-learned"></a>
### 5. Discussion and Lessons Learned

* **SEAL encryption is powerful but opaque:** The non-determinism and complexity of CKKS encryption makes it incompatible with NLP token-based models in its raw form.
* **Simulation can be effective:** While actual encryption was impractical, our controlled simulation preserved the research goal and allowed robust experimentation.
* **Visual tools matter:** Loss/accuracy curves and confusion matrices exposed model behaviors that raw metrics alone would not.
* **ONNX export is a key milestone:** Generating and validating an inference-ready model opens doors for deployment or benchmarking beyond the research setting.

---

<a id="conclusion"></a>
### 6. Conclusion

Module 2 was a critical step in maturing the project. The limitations of real homomorphic encryption in the context of neural inference—especially in NLP—forced a methodological shift toward simulation. By implementing a deterministic randomized mapping of token IDs, we preserved the privacy-preserving spirit of the project while unlocking the ability to train, evaluate, and export the model effectively.
The article draft was significantly updated to reflect this pivot and is now structurally ready for submission, pending additional experiments in Module 3.

---
