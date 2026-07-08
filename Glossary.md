# Glossary

PQC 세미나 학습 중 새로 나온 용어 누적 정리.

## Lattice-Based Cryptography (1강 Introduction)

- **MLWE (Module Learning With Errors)**: LWE 문제를 모듈(module) 구조 위로 일반화한 문제. Ring-LWE보다 유연한 파라미터 선택이 가능해 Kyber(ML-KEM)의 안전성 근거로 쓰임.
- **D-MLWE (Decisional MLWE)**: MLWE의 결정(decisional) 버전 — 주어진 샘플이 MLWE 분포에서 나온 것인지 균등 분포에서 나온 것인지 구별하는 문제. Kyber(ML-KEM)는 D-MLWE에, Dilithium(ML-DSA)은 D-MLWE와 MSIS에 안전성을 근거함.
- **MSIS (Module Short Integer Solutions)**: SIS 문제를 모듈 구조 위로 일반화한 문제. Dilithium(ML-DSA)의 안전성 근거 중 하나 (D-MLWE와 함께).
