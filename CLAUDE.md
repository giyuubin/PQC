# PQC 세미나 프로젝트

정보보호학과 학부연구생(ISNPL) 세미나 학습 프로젝트. 현대암호학 세미나를 마치고 PQC(Post-Quantum Cryptography)를 공부 중.

현재 커리큘럼은 Alfred Menezes 교수의 Cryptography 101 강의 시리즈(cryptography101.ca)를 따른다:

1. **Lattice-Based Cryptography** (진행 중 — 아래 7강)
2. Kyber and Dilithium (ML-KEM, ML-DSA) — 다음 단계
3. Hash-Based Signature Schemes (LMS, XMSS, SPHINCS+/SLH-DSA) — 그 다음 단계

## 폴더 구조 및 실제 내용

- `Lecture slides/` — Lattice-Based Cryptography 코스의 강의 슬라이드 7개:
  1. Introduction
  2. SIS (Short Integer Solutions)
  3. LWE (Learning With Errors)
  4. Lattices
  5. SIS/LWE and Lattices
  6. Ring-SIS and Ring-LWE
  7. Module-SIS and Module-LWE
- `Papers/` — 교재 PDF: *A Gentle Introduction to Lattice-Based Cryptography* (이 코스의 공식 lecture notes, 7강 전체를 커버함). 학습 시 슬라이드와 이 교재를 함께 대조해서 참조할 것.
- `Notes/` — 정리 요약 (마크다운). 강의 번호/제목과 매칭해서 저장 (예: `Notes/3. LWE.md`)
- `presentation/` — 세미나 발표용으로 직접 만드는 결과물 저장 위치 (pptx 초안, 발표 스크립트 등)
- `Glossary.md` — 새로 나온 용어 누적 정리 (SIS, LWE, Module-LWE, NTT, ML-KEM, ML-DSA 등)
- `.claude/commands/` — `study.md`, `slides.md` 커스텀 커맨드

## 공통 규칙

- 답변은 간결하고 직접적으로. 불필요한 수식어나 장황한 설명 지양.
- 암호학 표기법은 정확하게 사용 (SIS, LWE, Ring-LWE, Module-LWE, NTRU, ML-KEM, ML-DSA, LMS, XMSS, SPHINCS+/SLH-DSA 등 표준 용어).
- 강의 슬라이드에 알려진 오류(errata)가 있을 수 있음 — 교재(Papers) 내용과 다르면 교재를 우선 신뢰하고 사용자에게 알려줄 것.
- 새로운 개념이 나오면 `Glossary.md`에 추가할지 물어보고 반영.
- NIST 표준(FIPS 203/204/205) 등 최신 정보가 필요하면 검색으로 확인 후 답변.
