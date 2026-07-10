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

## Lattice-Based Cryptography (2강 SIS)

- **SIS (Short Integer Solutions, 최단 정수해 문제)**: 균등 랜덤 행렬 $A \in \mathbb{Z}_q^{n\times m}$가 주어졌을 때 $Az \equiv 0 \pmod q$, $z\neq 0$, $z\in[-B,B]^m$을 만족하는 짧은 벡터 $z$를 찾는 문제. Ajtai가 1996년 도입. Dilithium(ML-DSA)의 안전성 근거인 MSIS(Module-SIS)의 기반이 되는 문제.
- **ISIS (Inhomogeneous SIS, 비동차 최단 정수해 문제)**: SIS의 우변이 $0$이 아닌 랜덤 벡터 $b$인 버전 — $Az \equiv b \pmod q$, $z\in[-B,B]^m$. SIS와 계산적으로 동치(다항식 시간 상호 환원 가능).
- **nf-ISIS (Normal-form ISIS, 정규형 ISIS)**: $[A\mid I_n]z \equiv b \pmod q$ 형태의 ISIS. $\mathrm{ISIS}(n,m+n,q,B)$와 동치.
- **충돌 저항 해시 함수 (Collision-Resistant Hash Function)**: 서로 다른 두 입력이 같은 출력으로 매핑되는 충돌(collision)을 찾기 어려운 해시 함수. $H_A(z)=Az \bmod q$ (단, $A\in\mathbb{Z}_q^{n\times m}$, $m>n\log_2 q$)는 SIS$(n,m,q,1)$이 어렵다는 가정 하에 충돌 저항적임 — 충돌을 찾으면 곧 SIS 해를 찾은 것이 되기 때문.
- **비둘기집 원리를 이용한 환원 (Reduction via Pigeonhole Principle)**: 후보 집합의 크기가 목표 공간의 크기보다 크면($(B+1)^m > q^n$ 등) 서로 다른 두 후보가 반드시 같은 값으로 충돌한다는 논증. SIS 해의 존재성을 증명할 때 사용 — $z_1\neq z_2$가 $Az_1\equiv Az_2 \pmod q$를 만족하면 $z=z_1-z_2$가 SIS 해가 됨.
