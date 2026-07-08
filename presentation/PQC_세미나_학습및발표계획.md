# PQC 세미나 학습 및 발표 계획

정보보호학과 학부연구생 (ISNPL) — Post-Quantum Cryptography 학습 로드맵
작성일: 2026-07-08

## 1. 개요

현대암호학 세미나를 마치고, Post-Quantum Cryptography(PQC) 학습을 시작한다. 커리큘럼은 Alfred Menezes 교수(University of Waterloo)의 Cryptography 101 강의 시리즈(cryptography101.ca)를 따른다. 총 3개 코스, 17개 세부 강의로 구성되며, 아래 순서로 학습을 진행한다.

- Lattice-Based Cryptography (7강) — 격자 기반 암호의 수학적 기초 (SIS, LWE, Ring/Module 변형)
- Kyber and Dilithium (4강) — NIST 표준 ML-KEM, ML-DSA의 구체적 구성과 최적화
- Hash-Based Signature Schemes (6강) — LMS, XMSS, SPHINCS+(SLH-DSA)

세 코스는 난이도와 선후 관계상 이 순서로 배치했다. Lattice-Based Cryptography에서 다지는 SIS/LWE/Module-LWE 개념이 Kyber·Dilithium 이해의 전제 조건이며, Hash-Based Signature는 격자 이론과 독립적이라 마지막에 배치해도 무리가 없다.

## 2. 학습 목표

각 코스의 공식 learning outcomes를 기준으로 삼는다.

- **Lattice-Based Cryptography**: 격자의 정의와 기본 성질, SVP/SIVP 등 격자 문제, SIS·LWE·Module-SIS·Module-LWE와 격자의 연결 관계를 이해한다.
- **Kyber and Dilithium**: Kyber PKE/KEM과 Dilithium 서명 스킴의 동작 원리, 성능 최적화 기법을 이해하고 FIPS 203/204 표준 문서를 직접 읽고 이해할 수 있는 수준에 도달한다.
- **Hash-Based Signature Schemes**: LMS·XMSS·SPHINCS+의 핵심 구성 요소와 동작 원리를 이해하고, RFC 8554·RFC 8391·FIPS 205를 읽고 이해할 수 있는 수준에 도달한다.

## 3. 전체 일정표

7월 9일 세미나에서 본 계획을 발표한다. 7~8월은 화·목 주 2회로 진행하며, 8월 18·20·25일은 세미나가 없다. 9월부터는 2주에 1회로 전환되고, 10월 20~26일 중간고사 2주 전부터는 세미나를 하지 않는다.

배분 원칙:

- 화요일은 목요일 세미나 이후 나흘(금~월)의 준비 기간이 있어 상대적으로 더 많은 분량을 담을 수 있다. 목요일은 준비 기간이 이틀(화~수)뿐이라 가볍게 유지한다.
- 정말 분량이 많거나 어려운 회차(Ring-SIS/Ring-LWE, Kyber V2, Dilithium)는 화·목이 함께 있는 주에 한해 화요일에 시작해 목요일에 끝낸다.
- Introduction 성격의 강의(V1)는 화요일 세미나가 있는 주의 목요일에 배치한다.
- 화·목이 둘 다 있는 시기가 끝난 뒤(8월 27일 이후)는 세션 간 공백이 길수록(2주 이상) 한 세션에 담는 분량을 늘린다.

전체 학습은 **10월 1일 완료**를 목표로 한다.

| 날짜 | 요일 | 코스 | 회차 | 주제 |
|---|---|---|---|---|
| 2026-07-09 | 목 | 발표 + Lattice-Based Crypto | 계획 발표 + 1강 | 학습 로드맵/일정표 발표 및 1강 Introduction (정식 학습) |
| 2026-07-14 | 화 | Lattice-Based Crypto | 2강+3강+4강 | SIS (10p) + LWE (18p) + Lattices (19p) — 목요일 세미나 이후 나흘(금~월) 공백이라 세 회차 결합 |
| 2026-07-16 | 목 | Lattice-Based Crypto | 5강 | SIS/LWE and Lattices (19p) — 다음 6강을 화요일에 시작하기 위해 단독 진행 |
| 2026-07-21 | 화 | Lattice-Based Crypto | 6강 (1/2) | Ring-SIS and Ring-LWE — 전반부 (29p, errata 12개로 최다 — 화요일 시작, 목요일 종료) |
| 2026-07-23 | 목 | Lattice-Based Crypto | 6강 (2/2) | Ring-SIS and Ring-LWE — 후반부 |
| 2026-07-28 | 화 | Lattice-Based Crypto | 7강 | Module-SIS and Module-LWE (19p) |
| 2026-07-30 | 목 | Kyber & Dilithium | V1 | Introduction 전체 (PQC 개요 + 수학적 사전지식, 41p) — 화요일(7/28) 세미나가 있는 주의 목요일이라 조건 충족, 분할 없이 진행 |
| 2026-08-04 | 화 | Kyber & Dilithium | V2 (1/2) | Kyber PKE (simplified) + 최적화 (38p — 화요일 시작, 목요일 종료) |
| 2026-08-06 | 목 | Kyber & Dilithium | V2 (2/2) | Kyber PKE (full scheme) + KEM |
| 2026-08-11 | 화 | Kyber & Dilithium | V3 (1/2) | Dilithium 토이 버전 + t 압축 없는 버전 (58p, 최장·errata 최다 — 화요일 시작, 목요일 종료) |
| 2026-08-13 | 목 | Kyber & Dilithium | V3 (2/2) | Dilithium t 압축 + 전체 스킴 |
| 2026-08-27 | 목 | Kyber & Dilithium | V4 | NTT — Dilithium NTT + Kyber NTT 결합 (8/13 이후 화요일 없이 2주 공백이라 결합) |
| 2026-09-03 | 목 | Hash-Based Signatures | V1+V2+V3 | Introduction + Hash functions + Lamport 서명 — 코스 전체가 가벼워 세 항목 결합 |
| 2026-09-17 | 목 | Hash-Based Signatures | V4+V5 | Lamport 서명 문제점과 해결책 + LMS — 9/3 이후 2주 공백이라 결합 |
| 2026-10-01 | 목 | Hash-Based Signatures | V6 | SPHINCS+ / SLH-DSA (17p) — 마지막 회차 |

## 4. 학습 방식

각 세션은 강의 슬라이드와 공식 교재(*A Gentle Introduction to Lattice-Based Cryptography* 등)를 대조하며 진행한다. 수식은 정의부터 유도 과정까지 직접 전개해보고, 작은 숫자 예제로 검증한다. 매 세션 종료 후 이해도 확인 문제를 풀고, 학습 내용은 정리 노트로 남긴다.

## 5. 향후 계획

10월 1일 커리큘럼을 완료한 뒤에는 세 코스 중 가장 흥미를 느낀 주제(또는 지도교수님과 상의한 주제)를 선정하여 심화 학습하고, 이를 바탕으로 정식 세미나 발표를 준비할 예정이다. 후보로는 다음을 고려하고 있다.

- Module-LWE 기반 최신 공격 기법 동향 (lattice reduction, 격자 축소 알고리즘)
- ML-KEM/ML-DSA의 실제 구현 최적화 (NTT 기반 다항식 곱셈 등)
- 해시 기반 서명의 상태 관리(stateful) 문제와 SPHINCS+의 stateless 설계 비교

구체적인 심화 주제는 학습을 진행하며 지도교수님과 논의 후 확정한다.
