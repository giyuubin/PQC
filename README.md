# PQC Seminar Study Project

A study repository for an Information Security / Smart Security (ISPL) undergraduate research seminar. Having completed a seminar on modern cryptography, currently studying Post-Quantum Cryptography (PQC).

## Curriculum

Following Prof. Alfred Menezes' (University of Waterloo) [Cryptography 101](https://cryptography101.ca) lecture series, studied in the following order. Lecture counts per course aren't tracked here, since Menezes may add lectures to a course over time — the most recent file in `Notes/` reflects both the current lecture count and where progress currently stands.

1. **Lattice-Based Cryptography** — Mathematical foundations of lattice-based cryptography (SIS, LWE, Ring/Module variants)
2. **Kyber and Dilithium** — Concrete construction and optimization of the NIST standards ML-KEM and ML-DSA
3. **Hash-Based Signature Schemes** — LMS, XMSS, SPHINCS+ (SLH-DSA)

The SIS/LWE/Module-LWE concepts built in the first course are prerequisites for understanding Kyber and Dilithium, while Hash-Based Signatures are independent of lattice theory and are therefore placed last. Lecture numbers continue sequentially across course boundaries (e.g. if course 1 ends at lecture 7, course 2 starts at lecture 8). The overall study plan targets **completion by October 1, 2026**. See [presentation/0709_1_Introduction.pdf](presentation/0709_1_Introduction.pdf) for the seminar orientation slides.

## Folder Structure

```
.
├── Lecture slides/   # Lecture slide PDFs, per course (copyrighted material — gitignored, not included in this repo)
├── Papers/           # Textbook PDFs (copyrighted material — gitignored, not included in this repo)
├── Notes/            # Study notes, one per lecture (markdown)
├── presentation/     # Seminar presentation materials (plans, slide drafts, etc.)
└── Glossary.md       # Cumulative glossary of terms encountered during study
```

`Lecture slides/` and `Papers/` are copyrighted material from Prof. Alfred Menezes (cryptography101.ca) and are kept locally only, not redistributed.

## Study Approach

Each session is driven by the lecture video (Cryptography 101 on YouTube) as the sole primary source — the video already shows the lecture slides on screen, so the local `Lecture slides/` copy isn't cross-referenced separately (it only becomes the primary source for the rare session with no video link). The textbook (`Papers/`) is consulted only to supplement material the video doesn't cover, and is cited by page/location with a one-line summary rather than reproduced in the notes; the course-to-textbook mapping is recorded in each course's first note. Content is reorganized by conceptual/logical dependency rather than the source's original order. Formulas are derived from definitions step by step and verified with small numerical examples. After each session, comprehension questions are worked through and a structured summary note is saved.

## Reference Documents

- [presentation/0709_1_Introduction.pdf](presentation/0709_1_Introduction.pdf) — Seminar orientation slides
- [Glossary.md](Glossary.md) — Glossary of terms
