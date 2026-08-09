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

## Lattice-Based Cryptography (7강 Module-SIS and Module-LWE)

- **모듈 (Module, $R_q^k$)**: 벡터공간(vector space)의 스칼라 체(field)를 링(ring)으로 바꾼 대수 구조. $R_q^k$는 $R_q=\mathbb{Z}_q[x]/(x^n+1)$의 원소를 성분으로 갖는 길이 $k$ 벡터 전체의 집합이며, 덧셈·뺄셈은 성분별로, 내적(inner product)은 $R_q$의 원소(다항식) 하나를 만든다. MSIS·MLWE의 무대가 되는 구조.
- **MSIS (Module Short Integer Solutions, $\mathrm{MSIS}(n,k,\ell,q,B)$)**: SIS를 모듈 위로 일반화한 문제 — $a_1,\dots,a_\ell\in_RR_q^k$($\ell>k$)가 주어졌을 때 $a_1z_1+\cdots+a_\ell z_\ell=0$, $\|z_i\|_\infty\le B$인 $0$이 아닌 $z_i\in R_q$를 찾는다. 행렬 형태로는 $A$가 $k\times\ell$개의 anti-circulant 블록으로 이루어진 구조화된 SIS. $k=1$이면 Ring-SIS, $n=1$이면 SIS가 되어 둘 사이를 보간한다. Langlois-Stehlé(2015) 도입, 모듈 격자에서의 근사-$\mathrm{SVP}_\gamma$로부터의 (고전적) worst-case to average-case 환원을 가짐. Dilithium(ML-DSA)의 안전성 근거.
- **MLWE (Module Learning With Errors, $\mathrm{MLWE}(n,k,\ell,q,B)$)**: LWE를 모듈 위로 일반화한 문제 — $s\in_RR_q^\ell$, $e\in_RS_B^k$($k>\ell$)이고 $a_1,\dots,a_k\in_RR_q^\ell$, $b_i=a_i^\top s+e_i$일 때 $s$를 찾는다. 행렬 형태로는 $A$가 anti-circulant 블록으로 구조화된 LWE. $\ell=1$이면 Ring-LWE, $n=1$이면 LWE가 되어 둘 사이를 보간한다. Brakerski-Gentry-Vaikuntanathan(2011) 도입, Langlois-Stehlé(2015)가 모듈 격자에서의 근사-$\mathrm{SVP}_\gamma$로부터의 양자 환원을 증명(단, 매우 비타이트). Kyber(ML-KEM)의 안전성 근거.
- **ss-MLWE / ss-D-MLWE (Short-secret (Decisional) MLWE, 짧은 비밀 (결정) MLWE)**: 비밀 $s$도 오차 $e$처럼 작은 계수($S_{\eta_1}^\ell$)에서 뽑는 MLWE·D-MLWE 변형. 일반 MLWE와 계산적으로 동치. Kyber-PKE의 키 생성(공개키 $(A,b)$에서 개인키 $s$를 복원하는 것이 ss-MLWE 인스턴스)과 IND-CPA 안전성(ss-D-MLWE의 어려움에 근거)에 직접 쓰인다.
- **Kyber-PKE**: Kyber(ML-KEM)의 바탕이 되는 공개키 암호 스킴 — Lindner-Peikert 암호(3강)를 모듈 $R_q^k$로 확장한 것. $q=3329$, $n=256$을 고정하고 $k\in\{2,3,4\}$로 보안 수준을 조절하며, 한 번에 $256$비트를 암호화한다. IND-CPA 안전성은 ss-D-MLWE의 어려움에 근거(교재 Theorem 6.4). Kyber-KEM은 이 Kyber-PKE에 Fujisaki-Okamoto류 변환을 적용해 만든다.

## Kyber and Dilithium (8강 Kyber and Dilithium)

- **큐비트 (Qubit)**와 **중첩 (Superposition)**: 큐비트는 고전 비트의 양자 대응물로, $0$과 $1$ 두 상태를 동시에(각각 어떤 확률로) 가질 수 있다 — 이 현상이 중첩. $n$큐비트 레지스터는 $2^n$개 상태 전부를 동시에 취할 수 있지만, 측정(measure)하는 순간 확률분포에 따라 그중 하나로 붕괴해 관측 가능한 출력은 단 하나뿐이다.
- **Shor의 알고리즘 (Shor's Algorithm)**: 정수 인수분해·이산로그·타원곡선 이산로그(ECDLP)를 모두 양자 다항식 시간에 푸는 알고리즘(1994). RSA·이산로그·ECC 기반 공개키 암호 전체를 무너뜨리는 양자컴퓨터의 주된 위협.
- **Grover의 알고리즘 (Grover's Algorithm)**: 비구조화 탐색(unstructured search) 문제를 고전 알고리즘의 제곱근 시간($\sqrt{2^n/d}$번의 함수 평가)에 푸는 양자 알고리즘(1996). AES 같은 블록암호에 대한 전수조사를 $2^{\ell/2}$번으로 가속하지만, 병렬화해도 선형으로 빨라지지 않는다. 대응책은 키 길이를 두 배(예: AES-256)로 늘리는 것.
- **CNSA 2.0 (Commercial National Security Algorithms 2.0)**: 2022년 NSA가 발표한 양자 안전 알고리즘 스위트. 서명에 Dilithium, 키 캡슐화에 Kyber, 소프트웨어·펌웨어 서명에 해시 기반 서명 LMS·XMSS를 지정(대칭키 AES·SHA는 유지). CNSA 1.0(ECDSA·RSA 기반)을 대체하며, 전환 시한이 매우 공격적(예: 소프트웨어 서명 2030년까지 전면 전환).
- **FIPS 205 (SPHINCS+/SLH-DSA)**: NIST가 2024년 8월 FIPS 203(Kyber)·FIPS 204(Dilithium)와 함께 발표한 세 번째 양자 안전 표준 — 상태를 저장하지 않는(stateless) 해시 기반 전자서명 스킴 SPHINCS+의 공식 명세(공식 이름 SLH-DSA, Stateless Hash-Based Digital Signature Algorithm). Kyber·Dilithium과 달리 격자가 아니라 해시 함수의 안전성에만 의존한다.
- **D-MLWE (Decisional Module-LWE, 결정적 모듈-LWE)**: $A\in_RR_q^{k\times\ell}$가 주어졌을 때, $z=As+e$($s,e$가 작은 벡터, MLWE 인스턴스)인지 $z$가 완전히 무작위인 $R_q^k$ 벡터인지 구별하는 문제 — MLWE(탐색 버전, 비밀 $s$를 복원)의 결정 버전. Kyber-PKE의 IND-CPA 안전성이 정확히 이 문제의 어려움에 근거한다(비밀도 작다는 조건을 추가한 특수 경우가 ss-D-MLWE, 7강 참고).

## Kyber and Dilithium (9강 Kyber-PKE)

- **가장 가까운 정수 표기 $\lceil x\rfloor$ (Nearest Integer, Ties Broken Upward)**: $x$에 가장 가까운 정수를 나타내되, 동점(예: $x=13.5$)인 경우 위로 반올림하는 함수. $\mathrm{Round}_q$, $\mathrm{Compress}_q$/$\mathrm{Decompress}_q$, 메시지 스케일링($\lceil q/2\rfloor m$) 등 Kyber 전반에서 반복적으로 쓰인다.
- **$\mathrm{Compress}_q$ / $\mathrm{Decompress}_q$ (암호문 압축/압축해제)**: 정수 $X\in[0,q-1]$을 $d$비트($d<\lceil\log_2q\rceil$)로 반올림해 저장 공간을 줄이는 손실 압축 함수. $\mathrm{Compress}_q(X,d)=\lceil(2^d/q)X\rfloor\bmod2^d$, $\mathrm{Decompress}_q(Y,d)=\lceil(q/2^d)Y\rfloor\bmod q$. Kyber 암호문의 $u,v$ 성분에 계수별로 적용해 암호문 크기를 대폭 줄이며, 그 대가로 복호화 오차가 약간 늘어난다.
- **중심 이항분포 (Central Binomial Distribution, CBD)**: $\eta$쌍의 균등 무작위 비트 $(a_i,b_i)$에 대해 $c=\sum_{i=1}^\eta(a_i-b_i)$로 정의되는 분포. Kyber가 비밀·오차 다항식의 계수를 뽑을 때 균등분포 대신 사용 — 정수 개수가 $2$의 거듭제곱이 아닌 구간 $[-\eta,\eta]$에서의 거부 샘플링(rejection sampling)을 피할 수 있어 상수 시간 구현에 유리하다.

## Kyber and Dilithium (10강 Kyber-PKE 완성형과 Kyber-KEM)

- **키 캡슐화 메커니즘 (Key Encapsulation Mechanism, KEM)**: 두 당사자가 공유 비밀키를 수립하도록 해주는 프로토콜. 키생성·캡슐화(encapsulation)·역캡슐화(decapsulation) 세 알고리즘으로 구성되며, 공개키 암호(PKE)의 암호화/복호화와 달리 캡슐화 알고리즘이 평문을 자유롭게 고르는 대신 비밀키 $K$ 자체를 생성해 낸다.
- **캡슐화 키 / 역캡슐화 키 (Encapsulation Key, $ek$ / Decapsulation Key, $dk$)**: KEM의 공개키·개인키에 대응하는 명칭. Kyber-KEM에서 $ek=(\rho,t)$(Kyber-PKE 공개키와 같음), $dk=(s,ek,H(ek),z)$(Kyber-PKE 개인키 $s$에 재암호화 검증용 $ek,H(ek)$와 역캡슐화 실패 대비용 비밀 $z$가 추가됨).
- **Fujisaki-Okamoto 변환 (Fujisaki-Okamoto Transform, FO 변환)**: 선택 평문 공격(CPA)에 안전한 공개키 암호를 선택 암호문 공격(CCA)에 안전한 스킴으로 바꾸는 일반적인 방법(1999). 암호화에 필요한 무작위성을 메시지와 공개키의 해시로부터 결정적으로 유도(역랜덤화)하고, 역캡슐화 시 재암호화해 암호문이 일치하는지 검증하는 방식으로 작동한다. Kyber-KEM은 Hofheinz-Hövelmanns-Kiltz의 변형을 사용해 Kyber-PKE로부터 구성된다.
- **평문 인지성 (Plaintext Awareness)**: 캡슐화를 수행한 주체가 이미 비밀키 $K$를 알고 있는 경우에만 역캡슐화가 무작위 대체키 $\bar K$가 아니라 $K$를 내놓는다는 성질. FO 변환이 CCA 안전성을 얻는 핵심 메커니즘 — 복호화 오라클에 임의의 암호문을 제출해도 공격자가 실질적인 정보를 얻지 못하게 한다.
- **IND-CCA (Indistinguishability under Chosen-Ciphertext Attack, 선택 암호문 공격 하 구별 불가능성)**: 공격자가 (도전 암호문을 제외한) 임의의 암호문을 복호화 오라클에 제출해 그 결과를 볼 수 있는 더 강한 공격 모델 하의 구별 불가능성. IND-CPA보다 강한 안전성 개념이며, Kyber-PKE는 IND-CPA만 만족하고 Kyber-KEM이 FO 변환을 통해 IND-CCA를 만족한다.
- **랜덤 오라클 모델 (Random Oracle Model, ROM)**: 해시 함수를 이상화된 블랙박스(입력마다 진짜 균등 무작위 출력을 내고, 같은 입력엔 항상 같은 출력을 내는 오라클)로 취급하고 그 가정 아래 안전성을 증명하는 방법론. Kyber-KEM의 IND-CCA 안전성 증명이 이 모델(및 양자 공격자를 포함하는 QROM)에 의존한다.

## Kyber and Dilithium (11강 Dilithium (토이 버전과 t 압축 없는 버전))

- **Schnorr 서명 스킴 (Schnorr Signature Scheme)**: 이산로그 문제의 어려움에 근거한 전자서명 스킴(1991). 커밋먼트 $w=g^y$, 챌린지 $c=H(M\|w)$, 응답 $z=y+ca$의 3단계 구조를 가지며, Dilithium 설계의 원형이다.
- **커밋먼트·챌린지·응답 (Commitment·Challenge·Response)**: Schnorr·Dilithium 서명 생성이 공유하는 3단계 골격. 서명자가 무작위성으로 커밋먼트를 만들고, 메시지와 커밋먼트를 해싱해 챌린지를 얻은 뒤, 비밀키와 챌린지로 응답을 계산한다.
- **Fiat-Shamir 방법론 (Fiat-Shamir Methodology/Transform)**: 대화형 신원 확인 스킴을 커밋먼트와 메시지를 함께 해싱해 비대화형 서명으로 바꾸는 일반적 기법. Schnorr·Dilithium의 "커밋먼트 → 챌린지 → 응답" 구조가 이 변환의 전형적인 형태다.
- **HighBits / LowBits (Decompose)**: 정수(또는 다항식 계수) $r$을 $r=r_1\alpha+r_0$($r_1=\mathrm{HighBits}$, $r_0=\mathrm{LowBits}$, $r_0$은 작은 나머지)로 분해하는 연산. Dilithium 검증자가 서명자의 커밋먼트 $w$ 자체가 아니라 $w-cs_2$만 계산할 수 있는 문제를, $cs_2$가 HighBits를 바꾸지 않을 만큼 작다는 사실을 이용해 우회하는 데 쓰인다.
- **비동차 MSIS / I-MSIS (Inhomogeneous MSIS)**: $Az\equiv b\pmod q$ ($b\ne0$인 짧은 $z$를 찾는 문제)인 MSIS의 비동차 버전. 행렬이 $[A\mid I_k]$ 꼴인 특수한 경우를 표준형(normal-form)이라 부른다. Dilithium의 위조(forgery) 난이도가 표준형 I-MSIS로 환원된다.
- **SHAKE256/SHAKE128, XOF (eXtendable-Output Function, 확장 가능 출력 함수)**: FIPS 202(SHA-3 표준)에 명시된 가변 길이 해시 함수. 출력 길이를 늘려도 앞부분이 그대로 유지되는 성질(XOF)을 가지며, Dilithium의 ExpandA·ExpandS·ExpandMask·$H$·SampleInBall 구현에 쓰인다.
- **ExpandA / ExpandS / ExpandMask**: 공개·비밀 시드로부터 각각 행렬 $A$, 서명키 $(s_1,s_2)$, 커밋먼트용 난수 $y$를 결정적으로 생성하는 의사난수 생성기(SHAKE 기반). 공개키·개인키 크기를 시드 하나로 줄이고(Kyber의 $A$ 생성과 같은 기법), 서명 과정을 결정적으로 만드는 데 쓰인다.
- **EUF-CMA (Existential Unforgeability under Chosen-Message Attack, 선택 메시지 공격 하 존재적 위조 불가능성)**: 전자서명 스킴의 표준 안전성 개념 — 공격자가 서명 오라클에 원하는 메시지를 질의해 서명을 받아볼 수 있어도, 질의하지 않은 새 메시지에 대한 유효한 서명은 위조할 수 없다는 성질. Dilithium은 D-MLWE·MSIS의 어려움과 랜덤 오라클 모델 가정 아래 EUF-CMA를 만족한다 — Kyber-KEM의 IND-CCA에 대응하는 서명 스킴 쪽의 강한 안전성 개념.
