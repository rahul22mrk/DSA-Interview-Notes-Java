# 🔢 Prime Numbers — Complete Notes (Striver's 5-Lecture Series)

> **Source:** Raj (Striver) | Prime Numbers for CP Playlist
> **Language:** Java | **Last Updated:** May 2026

---

## 📋 Table of Contents

- [L1 — Facts, Check Prime, Get Divisors](#-l1--facts-about-primes-check-prime-get-divisors)
- [L2 — Sieve of Eratosthenes](#-l2--sieve-of-eratosthenes)
- [L3 — Practice Problems on Sieve](#-l3--practice-problems-on-sieve)
- [L4 — Prime Factorisation](#-l4--prime-factorisation)
- [L5 — Segmented Sieve](#-l5--segmented-sieve)
- [Quick Revision Cheatsheet](#-quick-revision-cheatsheet)

---

## 📘 L1 — Facts about Primes, Check Prime, Get Divisors

🔗 [Watch Lecture](https://www.youtube.com/watch?v=FcsUvBywY1U&list=PLN4aKSfpk8TQDJz7KLiwGFgnoUUwzfl1i&index=1)

---

### 📌 Facts about Prime Numbers

- **2** is the only even prime number
- **2 and 3** are the only consecutive prime numbers
- Every prime > 3 can be written as **6k + 1 or 6k − 1** (where k is a natural number)
  - Example: 5 = 6(1)−1, 7 = 6(1)+1, 11 = 6(2)−1, 13 = 6(2)+1
- **Goldbach's Conjecture:** Every even integer > 2 can be expressed as sum of two primes
- **Wilson's Theorem:** (p − 1)! ≡ (p−1) mod p, for prime p
- 1 is **NOT** a prime (it has only 1 factor, itself)
- A prime number has **exactly 2 factors** — 1 and itself

---

### 📌 Divisors come in pairs

For any number n, divisors come in pairs `(i, n/i)`.
For n = 36: (1,36), (2,18), (3,12), (4,9), **[6×6]** ← middle pair when perfect square.

So we only need to loop till `√n` — the pairs mirror after that.

```
36: 1×36, 2×18, 3×12, 4×9, [6×6] | 9×4, 12×3, 18×2, 36×1
```

> ✅ Key insight: `i * i <= n` is equivalent to `i <= sqrt(n)` but avoids floating point

---

### ✅ Check if a Number is Prime

**Brute Force — O(n):**
Count all divisors from 1 to n. If count == 2, it's prime.

```java
// Brute: O(n)
public static boolean isPrimeBrute(int n) {
    if (n <= 1) return false;
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) cnt++;
    }
    return cnt == 2;
}
```

**Optimal — O(√n):**
Loop till √n. Count both `i` and `n/i` as divisors (if different).

```java
// Optimal: O(√n)
public static boolean isPrime(int n) {
    if (n <= 1) return false;
    int cnt = 0;
    for (int i = 1; (long) i * i <= n; i++) {
        if (n % i == 0) {
            cnt++;               // count i
            if (n / i != i)
                cnt++;           // count n/i only if different
        }
    }
    return cnt == 2;
}

// Cleaner version (no count):
public static boolean isPrimeClean(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n % 2 == 0 || n % 3 == 0) return false;
    for (int i = 5; (long) i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) return false;
    }
    return true;
}
```

**Time:** O(√n) | **Space:** O(1)

> 📝 **Why i += 6?** All primes > 3 are of form 6k±1. So we check i (= 6k−1) and i+2 (= 6k+1), skip the rest.

---

### ✅ Get All Divisors of a Number

**Brute — O(n):** loop 1 to n, collect all i where n%i==0

**Optimal — O(√n):**

```java
// Optimal: O(√n) + O(d log d) for sort
public static List<Integer> getDivisors(int n) {
    List<Integer> small = new ArrayList<>();
    List<Integer> large = new ArrayList<>();

    for (int i = 1; (long) i * i <= n; i++) {
        if (n % i == 0) {
            small.add(i);
            if (i != n / i)
                large.add(n / i);
        }
    }

    // merge: small is ascending, large is descending → reverse large
    for (int i = large.size() - 1; i >= 0; i--)
        small.add(large.get(i));

    return small;  // sorted result
}
```

**Time:** O(√n) | **Space:** O(d) where d = number of divisors

---

### ✅ Sum of Divisors of a Number

```java
// O(√n)
public static long sumOfDivisors(int n) {
    long sum = 0;
    for (int i = 1; (long) i * i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            if (i != n / i)
                sum += n / i;
        }
    }
    return sum;
}
```

**Time:** O(√n) | **Space:** O(1)

---

### 🧩 Practice Problem — 3 Prime Factors (n = a×b×c, a≠b≠c≠1)

**Problem:** Given n, find if it can be written as product of 3 **distinct** primes a×b×c (all ≠ 1).

**Approach:** Find smallest prime factor `a`, divide n by `a`, find smallest prime factor `b` of remaining, compute `c = n/(a*b)`, check all are distinct and c ≠ 1.

```java
// O(√n)
public static boolean hasThreePrimeFactors(int n) {
    // find smallest prime factor a
    int a = 1;
    for (int i = 2; (long) i * i <= n; i++) {
        if (n % i == 0) { a = i; break; }
    }
    if (a == 1) return false;  // n itself is prime, can't split

    n = n / a;

    // find smallest prime factor b from remaining n (b != a)
    int b = 1;
    for (int i = 2; (long) i * i <= n; i++) {
        if (n % i == 0 && i != a) { b = i; break; }
        if (n / i != i && n / i != a) { b = Math.min(b == 1 ? Integer.MAX_VALUE : b, n / i); }
    }
    if (b == 1) return false;

    int c = n / b;

    // all must be distinct and c != 1
    return a != b && b != c && a != c && c != 1;
}
```

> 📝 For n = 64: a=2, remaining=32, b=4 (not prime!), c=8 → c≠1 but b is not prime → INVALID
> For n = 30: 30 = 2×3×5 → a=2, b=3, c=5 → all distinct primes ✅

**Time:** O(√n) | **Space:** O(1)

---

## 📗 L2 — Sieve of Eratosthenes

🔗 [Watch Lecture](https://www.youtube.com/watch?v=QDFM7Mjk2mc&list=PLN4aKSfpk8TQDJz7KLiwGFgnoUUwzfl1i&index=2)

---

### 📌 Why Sieve?

**Problem:** T queries, each asking if n is prime. T ≤ 10⁶, n ≤ 10⁶.

- **Naive approach:** O(T × √n) = O(10⁶ × 10³) = O(10⁹) → **TLE** (limit is ~10⁸ ops/sec)
- **Sieve approach:** Precompute once in O(n log log n), then each query → O(1)

---

### 📌 How Sieve Works

Start with all numbers marked as prime (true). For each prime i:
- Mark all multiples of i as NOT prime
- Start from `i*i` (smaller multiples already handled by smaller primes)
- Outer loop only goes till `√N`

**Visual (N=25):**
```
2 → mark 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24...
3 → mark 6, 9, 12, 15, 18...  (6,12,18 already marked)
4 → already marked (composite), skip
5 → mark 10, 15, 20, 25... (10,15,20 already marked)
7 → 7*7=49 > 25, stop
```

Remaining unmarked: **2, 3, 5, 7, 11, 13, 17, 19, 23** ✅

---

### ✅ Sieve of Eratosthenes

```java
// O(N log log N) time | O(N) space
static final int N = 1_000_000;
static boolean[] sieve = new boolean[N + 1];

static void createSieve() {
    // Step 1: mark all as prime
    Arrays.fill(sieve, 2, N + 1, true);

    // Step 2: for each prime, mark its multiples
    for (int i = 2; (long) i * i <= N; i++) {
        if (sieve[i]) {
            for (int j = i * i; j <= N; j += i) {
                sieve[j] = false;
            }
        }
    }
}

// Usage: O(1) per query after O(N log log N) setup
public static void main(String[] args) {
    createSieve();
    // sieve[n] == true means n is prime
    System.out.println(sieve[13]);   // true
    System.out.println(sieve[15]);   // false
}
```

**Time:** O(N log log N) for setup, O(1) per query | **Space:** O(N)

> 📝 **Why start inner loop at i*i?**
> All composites less than i*i have already been marked by smaller primes.
> Example: for i=5, multiples 10=2×5, 15=3×5, 20=4×5 are already marked by 2,3,4.
> So start from 5×5=25.

> 📝 **Why outer loop till √N?**
> Any composite ≤ N must have a prime factor ≤ √N. So all composites are already marked by the time i > √N.

---

## 📙 L3 — Practice Problems on Sieve

🔗 [Watch Lecture](https://www.youtube.com/watch?v=-DHwP-oAV_0&list=PLN4aKSfpk8TQDJz7KLiwGFgnoUUwzfl1i&index=3)

---

### 🧩 Problem 1 — Check Prime with Multiple Queries

**Problem:** T test cases (T ≤ 10⁶), each gives n (n ≤ 10⁶). Print "Yes"/"No".

**Why naive fails:** O(T × √n) = O(10⁶ × 10³) = O(10⁹) → TLE

**Solution:** Sieve once, query in O(1).

```java
// O(N log log N) precompute + O(T) queries
static final int N = 1_000_000;
static boolean[] sieve = new boolean[N + 1];

static void createSieve() {
    Arrays.fill(sieve, 2, N + 1, true);
    for (int i = 2; (long) i * i <= N; i++) {
        if (sieve[i]) {
            for (int j = i * i; j <= N; j += i)
                sieve[j] = false;
        }
    }
}

public static void main(String[] args) {
    createSieve();                   // once: O(N log log N)
    Scanner sc = new Scanner(System.in);
    int t = sc.nextInt();
    while (t-- > 0) {
        int n = sc.nextInt();
        System.out.println(sieve[n] ? "Yes" : "No");   // O(1)
    }
}
```

**Time:** O(N log log N + T) | **Space:** O(N)

---

### 🧩 Problem 2 — Count Numbers with Min Prime Factor = n (SPOJ-style)

**Problem:** Given n, count how many numbers in [1, 10⁶] have **minimum prime factor = n**.

**Key Insight:** When sieve runs, whenever prime i marks composite j = i*i, i*i+i, ..., that prime i is the smallest prime factor of j (since we process primes in order).

**Modified Sieve — store count of times each number gets marked:**

```java
// O(N log log N)
static final int N = 1_000_000;
static int[] sieve = new int[N + 1];   // sieve[i] = 1 means prime, 0 means composite

static void createSieve() {
    // init all as 1 (prime)
    for (int i = 2; i <= N; i++) sieve[i] = 1;

    for (int i = 2; (long) i * i <= N; i++) {
        if (sieve[i] == 1) {
            for (int j = i * i; j <= N; j += i) {
                if (sieve[j] != 0) {
                    sieve[i]++;     // i is min prime factor of j
                    sieve[j] = 0;  // mark composite
                }
            }
        }
    }
}

// sieve[n] after createSieve() = count of numbers whose min prime factor is n
// Usage: System.out.println(sieve[2]) → count of even composites processed by 2
```

**Time:** O(N log log N) | **Space:** O(N)

---

### 🧩 Problem 3 — Finding the Kth Prime (SPOJ TDKPRIME)

🔗 [SPOJ Problem](https://www.spoj.com/problems/TDKPRIME/)

**Problem:** Q queries (Q ≤ 50000), each gives K (1 ≤ K ≤ 5×10⁶). Print the K-th prime.

**Approach:**
- Run sieve up to a large enough N (the 5×10⁶-th prime ≈ 86,028,121)
- Store all primes in a list `ds`
- Answer each query in O(1): `ds[k-1]`

```java
// O(N log log N) precompute + O(1) per query
static final int N = 86_028_121;   // covers first 5*10^6 primes
static boolean[] sieve = new boolean[N + 1];
static List<Integer> primes = new ArrayList<>();

static void createSieve() {
    Arrays.fill(sieve, 2, N + 1, true);
    for (int i = 2; (long) i * i <= N; i++) {
        if (sieve[i]) {
            for (int j = i * i; j <= N; j += i)
                sieve[j] = false;
        }
    }
    for (int i = 2; i <= N; i++) {
        if (sieve[i]) primes.add(i);
    }
}

public static void main(String[] args) {
    createSieve();
    Scanner sc = new Scanner(System.in);
    int q = sc.nextInt();
    while (q-- > 0) {
        int k = sc.nextInt();
        System.out.println(primes.get(k - 1));   // O(1)
    }
}
```

**Example:**
```
K=1  → 2
K=10 → 29
K=100 → 541
```

**Time:** O(N log log N + Q) | **Space:** O(N)

> 📝 Key: precompute sieve, store all primes in array `ds`, then `ds[k-1]` is O(1)

---

## 📕 L4 — Prime Factorisation

🔗 [Watch Lecture](https://www.youtube.com/watch?v=0DT1_B0PVak&list=PLN4aKSfpk8TQDJz7KLiwGFgnoUUwzfl1i&index=4)

---

### 📌 What is Prime Factorisation?

Every composite number can be broken down into prime factors:
```
30  = 2 × 3 × 5
48  = 2 × 2 × 2 × 2 × 3  = 2⁴ × 3
```

**Division tree for 48:**
```
48 ÷ 2 = 24
24 ÷ 2 = 12
12 ÷ 2 = 6
 6 ÷ 2 = 3
 3 ÷ 3 = 1
→ 48 = 2 × 2 × 2 × 2 × 3
```

---

### ✅ Method 1 — Trial Division (Brute)

```java
// O(N) per query — TLE for large N with many queries
public static void primeFactorisationBrute(int n) {
    for (int i = 2; i <= n; i++) {
        while (n % i == 0) {
            System.out.print(i + " ");
            n /= i;
        }
    }
    System.out.println();
}
```

**Time:** O(N) per query | **Space:** O(1)

---

### ✅ Method 2 — Optimised Trial Division

Loop only till √n. After loop, if n > 1, it's a prime factor itself.

```java
// O(√N) per query
public static void primeFactorisationOptimal(int n) {
    for (int i = 2; (long) i * i <= n; i++) {
        while (n % i == 0) {
            System.out.print(i + " ");
            n /= i;
        }
    }
    if (n > 1) System.out.print(n);   // remaining n is prime
    System.out.println();
}
```

**Example for n=35:**
```
i=2: 35%2≠0, skip
i=3: 35%3≠0, skip
i=4: 4*4=16 ≤ 35, 35%4≠0, skip
i=5: 35%5==0 → print 5, n=7; 7%5≠0, stop
Loop ends (6*6=36 > 7)
n=7 > 1 → print 7
Output: 5 7 ✅
```

**Time:** O(√N) per query | **Space:** O(1)

---

### ✅ Method 3 — Smallest Prime Factor (SPF) Sieve [FASTEST for multiple queries]

**Idea:** Precompute `spf[i]` = smallest prime factor of every number i.
Then for any query, factorize in O(log N) using spf array.

**How SPF sieve works:**
- Initialize `spf[i] = i` for all i
- For each prime i (where spf[i]==i), mark `spf[j] = i` for all multiples j = i*i, i*i+i, ...
  only if spf[j] hasn't been set yet (spf[j]==j means not yet assigned)

```
spf[1]=1, spf[2]=2, spf[3]=3, spf[4]=2, spf[5]=5,
spf[6]=2, spf[7]=7, spf[8]=2, spf[9]=3, spf[10]=2 ...
```

```java
// O(N log log N) precompute + O(log N) per query
static final int N = 1_000_000;
static int[] spf = new int[N + 1];   // smallest prime factor

static void createSPF() {
    for (int i = 1; i <= N; i++) spf[i] = i;   // init: spf[i] = i

    for (int i = 2; (long) i * i <= N; i++) {
        if (spf[i] == i) {   // i is prime (spf not updated = still itself)
            for (int j = i * i; j <= N; j += i) {
                if (spf[j] == j) {   // not yet assigned
                    spf[j] = i;      // i is the smallest prime factor of j
                }
            }
        }
    }
}

// Factorize any n in O(log N)
public static void primeFactorisationSPF(int n) {
    while (n != 1) {
        System.out.print(spf[n] + " ");
        n = n / spf[n];
    }
    System.out.println();
}

public static void main(String[] args) {
    createSPF();
    primeFactorisationSPF(30);   // 2 3 5
    primeFactorisationSPF(48);   // 2 2 2 2 3
}
```

**Time:** O(N log log N) precompute, O(log N) per query | **Space:** O(N)

---

### 🧩 Practice Problem — Print Prime Factorisation for T queries

**Problem:** T test cases (T ≤ 10⁶), each gives n (n ≤ 10⁶). Print prime factorisation of each n.

**Why naive fails:** O(T × √n) = O(10⁶ × 10³) = O(10⁹) → TLE

**Solution:** SPF sieve + O(log n) per query

```java
static final int N = 1_000_000;
static int[] spf = new int[N + 1];

static void createSPF() {
    for (int i = 1; i <= N; i++) spf[i] = i;
    for (int i = 2; (long) i * i <= N; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j <= N; j += i) {
                if (spf[j] == j) spf[j] = i;
            }
        }
    }
}

public static void main(String[] args) {
    createSPF();                    // O(N log log N) once
    Scanner sc = new Scanner(System.in);
    int t = sc.nextInt();
    while (t-- > 0) {
        int n = sc.nextInt();
        StringBuilder sb = new StringBuilder();
        while (n != 1) {
            sb.append(spf[n]).append(" ");
            n /= spf[n];
        }
        System.out.println(sb.toString().trim());   // O(log n) per query
    }
}
```

**Time:** O(N log log N + T log N) | **Space:** O(N)

---

## 📒 L5 — Segmented Sieve

🔗 [Watch Lecture](https://www.youtube.com/watch?v=MY0fXk-3BVQ&list=PLN4aKSfpk8TQDJz7KLiwGFgnoUUwzfl1i&index=5)

---

### 📌 Why Segmented Sieve?

**Problem:** Print all primes in range [L, R] where L, R ≤ 10¹², R−L ≤ 10⁶.

**Why regular sieve fails:**
- Regular sieve needs O(N) space = O(10¹²) array → **Memory Limit Exceeded**
- Even for N=10⁸ it's borderline (10⁸ booleans = 100 MB)

**Segmented sieve handles this** by:
- Running sieve only up to √R (≈ 10⁶) for small primes
- Using a small dummy array of size (R−L+1) for the actual range

---

### 📌 Algorithm — 3 Steps

```
Step 1: Generate all primes up to √R using regular sieve
Step 2: Create dummy array of size (R-L+1), initialize all to 1 (prime)
Step 3: For each prime p from Step 1:
           - Find first multiple of p in [L, R]
           - Mark all multiples of p in [L, R] as 0 (composite) in dummy array
Step 4: Remaining 1s in dummy array are primes in [L, R]
```

**Mapping:** `dummy[j - L]` corresponds to number `j` in range [L, R]

**Finding first multiple ≥ L:**
```
firstMultiple = ceil(L / p) * p = (L / p) * p
if firstMultiple < L: firstMultiple += p
also ensure firstMultiple != p itself (we don't mark the prime as composite)
→ use max(firstMultiple, p*p)
```

**Visual Example: L=110, R=130, primes=[2,3,5,7,11]**
```
dummy = [1,1,1,...,1]  (size 21, indices 0..20 = numbers 110..130)

prime=2: first multiple ≥ 110 = 110. Mark 110,112,114,...,130 as 0
prime=3: first multiple ≥ 110 = 111. Mark 111,114,117,...,129 as 0
prime=5: first multiple ≥ 110 = 110. Mark 110,115,120,125,130 as 0
prime=7: first multiple ≥ 110 = 112. Mark 112,119,126 as 0
prime=11: first = 121. Mark 121 as 0

Remaining 1s at indices: 3(=113), 7(=117 wrong)...
Actually primes in [110,130]: 113, 127
```

---

### ✅ Segmented Sieve — Java Implementation

```java
// O((R-L+1) log log R + √R log log √R) time | O(√R + R-L+1) space
public static List<Long> segmentedSieve(long L, long R) {
    int sqrtR = (int) Math.sqrt(R);

    // Step 1: Regular sieve up to sqrt(R)
    boolean[] smallSieve = new boolean[sqrtR + 1];
    Arrays.fill(smallSieve, true);
    smallSieve[0] = smallSieve[1] = false;
    for (int i = 2; (long) i * i <= sqrtR; i++) {
        if (smallSieve[i]) {
            for (int j = i * i; j <= sqrtR; j += i)
                smallSieve[j] = false;
        }
    }

    // Collect small primes
    List<Integer> smallPrimes = new ArrayList<>();
    for (int i = 2; i <= sqrtR; i++) {
        if (smallSieve[i]) smallPrimes.add(i);
    }

    // Step 2: Dummy array for range [L, R]
    int size = (int) (R - L + 1);
    boolean[] dummy = new boolean[size];
    Arrays.fill(dummy, true);   // assume all prime initially

    // Handle edge case: 1 is not prime
    if (L == 1) dummy[0] = false;

    // Step 3: Mark composites in [L, R]
    for (int p : smallPrimes) {
        // first multiple of p >= L
        long firstMultiple = ((L + p - 1) / p) * p;   // ceil(L/p)*p

        // don't mark the prime itself as composite
        if (firstMultiple == p) firstMultiple += p;

        // also start from max(firstMultiple, p*p)
        long start = Math.max(firstMultiple, (long) p * p);

        for (long j = start; j <= R; j += p) {
            dummy[(int) (j - L)] = false;
        }
    }

    // Step 4: Collect primes
    List<Long> result = new ArrayList<>();
    for (int i = 0; i < size; i++) {
        if (dummy[i]) result.add(L + i);
    }
    return result;
}

public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int t = sc.nextInt();
    while (t-- > 0) {
        long l = sc.nextLong();
        long r = sc.nextLong();
        List<Long> primes = segmentedSieve(l, r);
        for (long p : primes) System.out.print(p + " ");
        System.out.println();
    }
}
```

**Time:** O(√R · log log √R) for small sieve + O((R−L+1) · log log R) for marking
**Space:** O(√R) for small sieve + O(R−L+1) for dummy array

---

### 📌 Constraints & When to Use

| Constraint | Approach |
|---|---|
| n ≤ 10⁶, single query | Regular check O(√n) |
| n ≤ 10⁶, T ≤ 10⁶ queries | Regular Sieve O(n log log n) |
| n ≤ 10⁶, need factorisation for many queries | SPF Sieve |
| L, R ≤ 10¹², R−L ≤ 10⁶ | Segmented Sieve |

---

### 📌 Time Complexity Analysis (Segmented Sieve inner loop)

For prime p, multiples in [L, R] = **(R−L+1)/p + (R−L+1)/3 + (R−L+1)/5 + ...**

Total operations ≈ O((R−L+1) × log log R) — same as regular sieve but only for the segment size.

Memory used: O(√R + R−L+1) instead of O(R) → **huge saving**!

> 📝 For (L=10¹¹, R=10¹¹+10⁶): regular sieve needs 10¹¹ array → impossible.
> Segmented sieve needs only √(10¹¹) ≈ 316,228 + 10⁶ = manageable ✅

---

## 🗂️ Quick Revision Cheatsheet

| Technique | Use Case | Time | Space |
|-----------|----------|------|-------|
| Trial division `i*i<=n` | Check prime (single) | O(√n) | O(1) |
| 6k±1 trick | Check prime (faster) | O(√n) | O(1) |
| Sieve of Eratosthenes | Primes 1 to N, many queries | O(n log log n) | O(n) |
| SPF Sieve | Prime factorisation, many queries | O(n log log n) precompute + O(log n)/query | O(n) |
| Segmented Sieve | Primes in [L, R] with large L, R | O(√R log log R + (R-L) log log R) | O(√R + R-L) |

---

## 🧩 Key Patterns to Memorise

**Check Prime:**
```java
for (int i = 2; i * i <= n; i++)
    if (n % i == 0) return false;
return n > 1;
```

**Regular Sieve:**
```java
boolean[] sieve = new boolean[N + 1];
Arrays.fill(sieve, true);
sieve[0] = sieve[1] = false;
for (int i = 2; i * i <= N; i++)
    if (sieve[i])
        for (int j = i * i; j <= N; j += i)
            sieve[j] = false;
```

**SPF Sieve + Factorisation:**
```java
int[] spf = new int[N + 1];
for (int i = 0; i <= N; i++) spf[i] = i;
for (int i = 2; i * i <= N; i++)
    if (spf[i] == i)
        for (int j = i * i; j <= N; j += i)
            if (spf[j] == j) spf[j] = i;

// factorize n:
while (n != 1) { print(spf[n]); n /= spf[n]; }
```

**Segmented Sieve (inner loop key part):**
```java
long firstMultiple = ((L + p - 1) / p) * p;
if (firstMultiple == p) firstMultiple += p;
long start = Math.max(firstMultiple, (long) p * p);
for (long j = start; j <= R; j += p)
    dummy[(int)(j - L)] = false;
```
