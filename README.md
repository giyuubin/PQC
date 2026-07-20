# PQC Seminar Study Project

A study repository for an Information Security / Smart Security (ISPL) undergraduate research seminar. Having completed a seminar on modern cryptography, currently studying Post-Quantum Cryptography (PQC).

## Curriculum

Following Prof. Alfred Menezes' (University of Waterloo) [Cryptography 101](https://cryptography101.ca) lecture series. It consists of 3 courses and 17 lectures in total.

1. **Lattice-Based Cryptography** (7 lectures) — Mathematical foundations of lattice-based cryptography (SIS, LWE, Ring/Module variants) — *in progress*
2. **Kyber and Dilithium** (4 lectures) — Concrete construction and optimization of the NIST standards ML-KEM and ML-DSA
3. **Hash-Based Signature Schemes** (6 lectures) — LMS, XMSS, SPHINCS+ (SLH-DSA)

The three courses are studied in this order. The SIS/LWE/Module-LWE concepts built in the first course are prerequisites for understanding Kyber and Dilithium, while Hash-Based Signatures are independent of lattice theory and are therefore placed last. The overall study plan targets **completion by October 1, 2026**. See [presentation/PQC_세미나_OT.pptx](presentation/PQC_세미나_OT.pptx) for the seminar orientation slides.

## Folder Structure

```
.
├── Lecture slides/   # Lecture slide PDFs (copyrighted material — gitignored, not included in this repo)
├── Papers/           # Textbook PDFs (copyrighted material — gitignored, not included in this repo)
├── Notes/            # Study notes per lecture (markdown)
├── presentation/     # Seminar presentation materials (plans, slide drafts, etc.)
└── Glossary.md       # Cumulative glossary of terms encountered during study
```

`Lecture slides/` and `Papers/` are copyrighted material from Prof. Alfred Menezes (cryptography101.ca) and are kept locally only, not redistributed.

## Study Approach

Each session is driven primarily by the lecture video (Cryptography 101 on YouTube), cross-referenced against the lecture slides where a local copy exists; the textbook (*A Gentle Introduction to Lattice-Based Cryptography*) is used only to supplement material the video and slides don't cover. Content is reorganized by conceptual/logical dependency rather than the source's original order. Formulas are derived from definitions step by step and verified with small numerical examples. After each session, comprehension questions are worked through and a structured summary note is saved.

## Reference Documents

- [presentation/PQC_세미나_OT.pptx](presentation/PQC_세미나_OT.pptx) — Seminar orientation slides
- [Glossary.md](Glossary.md) — Glossary of terms
