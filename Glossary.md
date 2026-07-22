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
- **가우스 소거법과 SIS의 난이도 분리 (Gaussian Elimination vs. Short-Vector Search)**: $q$가 소수라 $\mathbb{Z}_q$가 체(field)이므로, $Az\equiv0\pmod q$의 해공간(=null space) 전체는 가우스 소거법으로 다항식 시간에 구할 수 있다 — 기약행사다리꼴로 만들면 피벗 변수를 자유변수들의 식으로 표현하는 파라메트릭 해가 즉시 나옴(예: 노트 Part 3.1, $z_1,z_2,z_3$을 $z_4,z_5$로 표현). SIS의 어려움은 이 null space를 "찾는" 데 있지 않고, 그 안에서 **모든 좌표가 $[-B,B]$에 속하는** 벡터를 찾는 데 있다 — 이는 격자의 (근사) 최단벡터문제(SVP)류에 해당하며 계산적으로 어렵다고 알려져 있음.
- **full column rank vs. full row rank (열/행 기준 최대 rank)**: $A\in\mathbb{Z}_q^{n\times m}$의 rank는 최대 $\min(n,m)$. **Full column rank**(rank $=m$, $m\le n$일 때 가능)는 "$m$개 열이 선형독립"과 동치이며, $z\mapsto Az$가 단사(injective)가 되어 $Az\equiv0\pmod q$의 해가 $z=0$뿐임을 의미 — SIS 노트 Part 2.1("$n\ge m$이면 해가 없다")이 여기 근거함. **Full row rank**(rank $=n$, $n\le m$일 때 가능)는 "$n$개 행이 선형독립"(동치로 열들이 $\mathbb{Z}_q^n$ 전체를 span)과 동치이며, $z\mapsto Az$가 전사(surjective)가 되어 임의의 $b$에 대해 $Az\equiv b\pmod q$가 항상 풀림을 의미 — 정상적인 SIS/ISIS 세팅($n<m$)에서 랜덤 행렬 $A$가 이 성질을 압도적 확률로 가짐. 노트 Part 3.1 예제의 RREF $A'$가 1,2,3열에 피벗 3개(=rank $3=n$, full row rank)를 가져서 자유변수가 $m-n=2$개(=$z_4,z_5$) 남는 것도 같은 원리.

## Lattice-Based Cryptography (3강 LWE)

- **LWE (Learning With Errors, 학습 오류 문제)**: 균등 랜덤 행렬 $A\in\mathbb{Z}_q^{m\times n}$($m\gg n$)와 $b=As+e\pmod q$($s\in\mathbb{Z}_q^n$은 비밀, $e\in[-B,B]^m$은 잡음)가 주어졌을 때 $s$를 찾는 문제. Regev가 2005년 도입. SIS와 달리 행렬이 "세로로 긴"($m\gg n$) 모양이며, 잡음 $e$ 때문에 가우스 소거법이 통하지 않는다. Kyber(ML-KEM)의 안전성 근거인 MLWE(Module-LWE)의 기반이 되는 문제.
- **DLWE (Decisional LWE, 결정 LWE)**: 주어진 $(A,c)$가 진짜 LWE 표본($c=As+e$)인지 균등 무작위($c=r$)인지 구별하는 문제. 탐색 문제인 LWE와 다항식 시간 상호 환원 가능(계산적으로 동치).
- **ss-LWE (Short-secret LWE, 짧은 비밀 LWE)**: 비밀 $s$도 오차 $e$처럼 $[-B,B]^n$에서 뽑는 LWE 변형. 일반 LWE와 달리 $m\gg n$ 없이도(심지어 $A$가 정사각행렬이어도) 해가 높은 확률로 유일하며, 일반 LWE와 계산적으로 동치. Lindner-Peikert 공개키 암호의 키 생성에 사용됨.
- **ss-DLWE (Short-secret Decisional LWE)**: ss-LWE의 결정 버전. Lindner-Peikert 공개키 암호의 IND-CPA 안전성이 이 문제의 어려움에 근거함.
- **Lindner-Peikert 공개키 암호 (Lindner-Peikert Public-Key Encryption, 2011)**: ss-DLWE의 어려움에 기반한 공개키 암호. $n\times n$ 정사각행렬 $A$만으로 키를 생성하고, 라운딩 함수(Round$_q$)로 비트 하나를 암호화·복호화한다. 다항식 링 $R_q$로 확장하면 Kyber 공개키 암호의 원형이 됨.
- **라운딩 함수 (Rounding Function, Round$_q$)와 대칭 mod ($\bmod_s q$)**: $\mathbb{Z}_q$의 원소를 $\{0,1\}$ 두 구간으로 반씩 나누는 함수. 대칭 mod는 $\mathbb{Z}_q$의 대표원을 $[-(q-1)/2,(q-1)/2]$로 표현하는 연산. Lindner-Peikert 암호의 복호화(잡음이 섞인 값에서 평문 비트를 복원)에 사용됨.
- **IND-CPA (Indistinguishability under Chosen-Plaintext Attack, 선택 평문 공격 하 구별 불가능성)**: 공격자가 평문을 골라 암호화 결과를 볼 수 있어도, 두 평문의 암호문을 구별할 수 없다는 안전성 개념. Lindner-Peikert 암호는 ss-DLWE가 어렵다는 가정 아래 IND-CPA를 만족함(단, 선택 암호문 공격(CCA)에는 별도 변환 없이는 안전하지 않음).

## Lattice-Based Cryptography (4강 Lattices)

- **격자 (Lattice)**: $\mathbb{R}^n$ 안의 선형독립인 $m$개 벡터의 모든 정수 선형결합의 집합. 이 벡터들의 집합을 기저(basis)라 부르고, 격자의 차원은 $n$, 랭크는 $m$이다. 기저 좌표가 모두 정수이면 정수 격자(integer lattice), 랭크가 $n$과 같으면 완전계수(full-rank) 격자라 한다.
- **부분격자 (Sublattice)**: 격자 $L$의 부분집합이면서 그 자체로도 격자인 것. $L'\subseteq L$이면 $L'$은 $L$의 부분격자.
- **기본평행육면체 (Fundamental Parallelepiped)**: 기저 $B=[b_1,\dots,b_n]$에 대해 계수를 $[0,1)$로 제한한 결합들의 집합 $P(B)$. $\mathbb{R}^n$을 겹치지 않는 영역으로 채우는 데 쓰이며, 그 "부피"가 격자의 부피와 같다.
- **유니모듈러 행렬 (Unimodular Matrix)**: 정수 성분을 갖고 행렬식이 $\pm1$인 정사각행렬. 같은 격자의 서로 다른 두 기저는 항상 유니모듈러 행렬로 연결된다(기저 특성화 정리).
- **격자의 부피 (Volume of a Lattice)**: $\mathrm{vol}(L)=|\det(B)|$ ($B$는 임의의 기저). 기저 선택에 무관한 격자의 불변량이며, 클수록 격자가 성기다(듬성듬성하다).
- **Successive minima (연속 최솟값)**: $i$번째 연속 최솟값 $\lambda_i(L)$은 $L$이 길이 $r$ 이하인 $i$개의 선형독립 벡터를 갖는 가장 작은 $r$. $\lambda_1(L)$은 최단 벡터의 길이.
- **Hermite 상수 (Hermite Constant)**와 **Minkowski의 정리 (Minkowski's Theorem)**: 둘 다 $\lambda_1(L)$을 $\mathrm{vol}(L)^{1/n}$으로 상계짓는 도구. Hermite의 상계는 지수적($\gamma_n\le(4/3)^{(n-1)/2}$), Minkowski의 정리는 선형적($\lambda_1(L)\le\sqrt n\,\mathrm{vol}(L)^{1/n}$)이라 훨씬 강하다.
- **가우스 휴리스틱 (Gaussian Heuristic)**: "무작위" 격자에서 $\lambda_1(L)\approx\sqrt{n/(2\pi e)}\,\mathrm{vol}(L)^{1/n}$이라는 근사식 — Minkowski 상계가 실전에서 거의 팽팽함을 시사.
- **LLL 알고리즘 (Lenstra-Lenstra-Lovász Algorithm)**: 주어진 (나쁜) 기저로부터 상대적으로 짧고 거의 직교하는 기저를 다항식 시간에 찾는 알고리즘(1982). 격자 기반 암호분석(예: DSA nonce 유출 공격)의 핵심 도구.
- **SVP (Shortest Vector Problem, 최단벡터문제)**: 격자의 0이 아닌 최단 벡터를 찾는 문제. NP-hard. 근사 버전 $\mathrm{SVP}_\gamma$는 길이 $\gamma\cdot\lambda_1(L)$ 이하인 벡터를 찾는 문제.
- **SIVP (Shortest Independent Vectors Problem, 최단독립벡터문제)**: $n$개의 선형독립 벡터를 모두 길이 $\lambda_n(L)$ 이하로 찾는 문제. 해가 반드시 기저를 이루는 것은 아님.
- **CVP (Closest Vector Problem, 최근접벡터문제)**: 격자 $L$과 목표 벡터 $t$가 주어졌을 때 $t$에 가장 가까운 격자점을 찾는 문제. Babai의 라운딩 알고리즘(LLL로 좋은 기저를 구한 뒤 반올림)으로 근사적으로 풀 수 있다.

## Lattice-Based Cryptography (5강 SIS/LWE and Lattices)

- **격자의 대안적 정의: 이산 가법 부분군 (Discrete Additive Subgroup)**: 격자 $L$을 "$\mathbb{R}^m$의 이산(discrete) 가법 부분군(additive subgroup)"으로 정의하는 방식 — 4강의 "선형독립 벡터들의 정수 선형결합" 정의와 동치이지만, $L_A^\perp=\{z:Az\equiv0\}$처럼 기저 후보 없이 방정식의 해 집합으로 주어진 대상이 애초에 격자인지 확인할 때 유용하다.
- **SIS 격자 (SIS Lattice, $L_A^\perp$)**: $\{z\in\mathbb{Z}^m : Az\equiv0\pmod q\}$, 즉 SIS 방정식의 해 전체(=$A$의 null space)로 이루어진 격자. 완전계수 $q$-ary 격자이며, 부피는 $q^n$이고, $A$를 행 축소해 얻은 기저 행렬은 삼각 블록 형태 $C=\begin{bmatrix}qI_n&-\bar A\\0&I_{m-n}\end{bmatrix}$를 갖는다. SIS는 이 격자에서의 근사-$\mathrm{SVP}_\gamma$와 동치다.
- **LWE 격자 (LWE Lattice, $L_A$)**: $\{y\in\mathbb{Z}^m : Az\equiv y\pmod q\text{인 }z\text{가 존재}\}$, 즉 $Az$로 표현 가능한 값들의 집합(=$A$의 mod $q$ 치역을 정수 전체로 확장한 것)으로 이루어진 격자. 완전계수 $q$-ary 격자이며, 부피는 $q^{m-n}$, 기저 행렬은 $D=\begin{bmatrix}I_n&0\\D_2&qI_{m-n}\end{bmatrix}$($D_2=A_2A_1^{-1}\bmod q$) 형태를 갖는다.
- **$q$-ary 격자 ($q$-ary Lattice)**: $q\mathbb{Z}^m\subseteq L\subseteq\mathbb{Z}^m$을 만족하는 격자 — 동치로, $z\in L \iff z\bmod q\in L$, 즉 격자 소속 여부가 $\bmod q$ 값만으로 결정된다. SIS 격자와 LWE 격자 모두 이 성질을 갖는다.
- **잉여류·몫군 (Coset · Quotient Group)**: 부분군(부분격자) $L$과 원소 $x$에 대해 $L$의 잉여류 $L+x=\{v+x:v\in L\}$; 서로 다른 잉여류 전체의 집합이 몫군 $\mathbb{Z}^m/L$이고 그 크기(지수)가 $|\mathbb{Z}^m/L|$이다. SIS 격자의 부피 $\mathrm{vol}(L_A^\perp)=q^n$을 증명할 때, 부피와 잉여류 개수가 같다는 사실(부분격자-부피 관계)이 핵심 도구로 쓰인다.
- **최악 케이스-평균 케이스 환원 (Worst-Case to Average-Case Reduction)**: "특정 (무작위) 인스턴스가 어렵다"는 평균 케이스 보장을, "모든 인스턴스 중 최악의 경우가 어렵다"는 (더 믿기 쉬운) 최악 케이스 가정으로부터 이끌어내는 환원. Ajtai(1996)가 SIS에 대해, Regev(2005)가 LWE에 대해 각각 근사-$\mathrm{SIVP}$(LWE의 경우 양자적으로)로부터의 환원을 증명했다 — 다만 두 환원 모두 점근적이고 비타이트(non-tight)해서 실전 파라미터 선택에는 직접 쓰이지 않는다.
- **BDD (Bounded Distance Decoding, 유한거리 복호화)**: 격자 $L$과 목표점 $b$가 주어졌을 때, $b$로부터 거리 $\alpha$ 이내에 있는 격자점 $y\in L$이 유일하다는 보장 하에 $y$를 찾는 문제. LWE 인스턴스 $(A,b)$는 $\alpha=\sqrt m B$인 $\mathrm{BDD}_\alpha$의 특수한 경우(단, $L_A$가 무작위가 아니라 $q$-ary인 특수 격자)로 재해석된다.
- **Kannan embedding과 프라이멀 공격 (Primal Attack)**: $\mathrm{BDD}_\alpha$ 인스턴스 $(L=L(D),b)$를 $(m{+}1)$차원 격자 $L'=L(D')$($D'=\begin{bmatrix}D&-b\\0&\alpha\end{bmatrix}$)에서의 SVP로 환원하는 기법. $\tilde v=(y-b,\alpha)$가 $L'$의 (사실상) 유일한 최단벡터가 되도록 구성되어, $L'$에서 SVP를 풀면 BDD의 답 $y$를 복원할 수 있다. LWE를 SVP 알고리즘(BKZ 등)으로 직접 공격하는 실전 기법의 이름이기도 하다.

## Lattice-Based Cryptography (6강 Ring-SIS and Ring-LWE)

- **다항식 링 (Polynomial Ring, $R=\mathbb{Z}[x]/(f)$)**: 정수 계수를 갖는 차수 $<n$ 다항식 전체의 집합. 덧셈·뺄셈은 성분별로, 곱셈은 모닉 다항식 $f$(차수 $n$)를 법으로 나눈 나머지로 정의한다. 계수도 $\bmod\,q$로 취급하면 $R_q=\mathbb{Z}_q[x]/(f)$ — Ring-SIS·Ring-LWE의 무대가 되는 대수 구조.
- **이상 (Ideal)** / **주 이상 (Principal Ideal)**: 이상은 덧셈·뺄셈에 닫혀 있고(가법 부분군) 링의 임의의 원소를 곱해도 닫혀 있는 $R$의 부분집합. 하나의 원소 $a(x)$가 생성하는 주 이상 $\langle a(x)\rangle=\{a(x)r(x)\bmod f(x):r(x)\in R\}$은 $a(x)$의 모든 배수로 이루어진다.
- **이상 격자 (Ideal Lattice)**: $R$의 (0이 아닌) 이상 $I$의 원소들을 벡터로 표현해 얻는 $\mathbb{R}^n$ 안의 정수 격자 $L(I)$. $f(x)=x^n-1$이면 순환 격자, $f(x)=x^n+1$이면 반순환 격자가 된다.
- **순환 격자 (Cyclic Lattice)** / **circulant 행렬**: $f(x)=x^n-1$일 때의 이상 격자 — 벡터가 우측 순환 시프트에 닫혀 있다. 주 이상의 기저 행렬은 circulant 행렬 $\mathrm{circ}(a)$(각 행이 이전 행의 순환 시프트)로 표현된다. Micciancio(2002)가 이를 이용한 압축 함수의 평균 케이스 원-웨이성을 증명했으나, 행의 합이 일정해 충돌 저항성은 없다.
- **반순환 격자 (Anti-Cyclic Lattice)** / **anti-circulant 행렬**: $f(x)=x^n+1$일 때의 이상 격자 — 순환 시프트에 부호 반전까지 더해진 구조. $n=2^w$이면 $x^n+1$이 기약다항식이라 완전계수 기저가 항상 보장된다는 것이 순환 격자 대비 장점. 기저 행렬은 anti-circulant 행렬 $\overleftarrow{\mathrm{circ}}(a)$. Ring-SIS·Ring-LWE가 실제로 채택하는 구조(Kyber·Dilithium의 $x^{256}+1$도 동일).
- **Ring-SIS**: SIS를 다항식 링 위로 일반화한 문제 — $a_1,\dots,a_\ell\in_R R_q$가 주어졌을 때 $a_1z_1+\cdots+a_\ell z_\ell\equiv0\pmod q$, $\|z_i\|_\infty\le B$인 $0$이 아닌 $z_i\in R_q$를 찾는다. 행렬 형태로 보면 $A$가 anti-circulant 블록으로 구조화된 SIS. Lyubashevsky-Micciancio-Peikert-Rosen(2006) 도입, 반순환 격자에서의 근사-$\mathrm{SVP}_\gamma$로부터의 worst-case to average-case 환원을 가짐. Module-SIS(MSIS)는 이를 모듈 랭크 $k>1$로 일반화한 것.
- **Ring-LWE**: LWE를 다항식 링 위로 일반화한 문제 — $s\in_RR_q$, $a_i\in_RR_q$가 주어지고 $b_i=a_is+e_i$($e_i$는 작은 오차)일 때 $s$를 찾는다. 비밀·오차가 벡터가 아니라 다항식 하나라 LWE보다 한 번에 더 많은 평문 비트($R_q$의 계수 하나마다 1비트)를 암호화할 수 있다. Lyubashevsky-Peikert-Regev(2010) 도입, 반순환 격자에서의 근사-$\mathrm{SVP}_\gamma$로부터의 양자 환원을 가짐. Module-LWE(MLWE)는 이를 비밀 벡터 차원 $\ell>1$로 일반화한 것(Kyber의 안전성 근거).
