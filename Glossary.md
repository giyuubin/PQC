# Glossary

PQC 세미나 학습 중 새로 나온 용어 누적 정리.

## Lattice-Based Cryptography (1강 Introduction)

- **MLWE (Module Learning With Errors)**: LWE 문제를 모듈(module) 구조 위로 일반화한 문제. Ring-LWE보다 유연한 파라미터 선택이 가능해 Kyber(ML-KEM)의 안전성 근거로 쓰임.
- **D-MLWE (Decisional MLWE)**: MLWE의 결정(decisional) 버전 — 주어진 샘플이 MLWE 분포에서 나온 것인지 균등 분포에서 나온 것인지 구별하는 문제. Kyber(ML-KEM)는 D-MLWE에, Dilithium(ML-DSA)은 D-MLWE와 MSIS에 안전성을 근거함.
- **MSIS (Module Short Integer Solutions)**: SIS 문제를 모듈 구조 위로 일반화한 문제. Dilithium(ML-DSA)의 안전성 근거 중 하나 (D-MLWE와 함께).
- **PQC (Post-Quantum Cryptography, 양자내성암호)**: 양자 컴퓨터를 이용한 공격에도 안전하도록 설계된 암호 체계 전반을 가리키는 용어. NIST가 2024년 8월 표준화한 스킴들이 대표적인 PQC.
- **Kyber (ML-KEM, Module-Lattice-based Key-Encapsulation Mechanism)**: NIST가 FIPS 203으로 표준화한 양자 안전 키 캡슐화 메커니즘. 안전성은 D-MLWE에 근거함.
- **Dilithium (ML-DSA, Module-Lattice-based Digital Signature Algorithm)**: NIST가 FIPS 204로 표준화한 양자 안전 전자서명 스킴. 안전성은 D-MLWE와 MSIS에 근거함.
- **FIPS 203 / FIPS 204**: NIST가 2024년 8월 발표한 연방 정보 처리 표준(Federal Information Processing Standards) 문서. 각각 ML-KEM(Kyber)과 ML-DSA(Dilithium)의 공식 명세.
