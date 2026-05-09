# Infosys SDE Sheet — DSA Revision Sheet
> **79 Problems | Pattern-wise | Java Solutions**  
> Easy: 39 | Medium: 22 | Hard: 14 | Total: 79

---

## Table of Contents
1. [Pattern 1 — Math / Logic / Basics](#pattern-1--math--logic--basics-29-problems)
2. [Pattern 2 — Two Pointers](#pattern-2--two-pointers-6-problems)
3. [Pattern 3 — Bit Manipulation](#pattern-3--bit-manipulation-2-problems)
4. [Pattern 4 — Sorting / Greedy](#pattern-4--sorting--greedy-7-problems)
5. [Pattern 5 — Sliding Window / Prefix Sum / Kadane's](#pattern-5--sliding-window--prefix-sum--kadanes-4-problems)
6. [Pattern 6 — HashMap / Frequency](#pattern-6--hashmap--frequency-3-problems)
7. [Pattern 7 — Binary Search](#pattern-7--binary-search-3-problems)
8. [Pattern 8 — Stack](#pattern-8--stack-2-problems)
9. [Pattern 9 — Dynamic Programming](#pattern-9--dynamic-programming-16-problems)
10. [Pattern 10 — Backtracking](#pattern-10--backtracking-1-problem)
11. [Pattern 11 — Linked List](#pattern-11--linked-list-1-problem)
12. [Pattern 12 — String Manipulation](#pattern-12--string-manipulation-5-problems)

---

---

## Pattern 1 — Math / Logic / Basics (29 problems)

> **When to use:** No fancy data structure needed. Pure formula, loops, or simple conditionals.  
> **Time:** Usually O(1) or O(n) | **Space:** O(1)

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 1 | Count Digits in a Number | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/count-digits-1606889545/1) |
| 2 | Print First N Fibonacci Numbers | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/print-first-n-fibonacci-numbers1002/1) |
| 3 | Program for Armstrong Numbers | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/armstrong-numbers2727/1) |
| 4 | Area of Rectangle, Right Triangle and Circle | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/area-of-rectange-right-angled-triangle-and-circle2600/1) |
| 5 | Check if Two Matrices are Identical | 🟢 Easy | O(m×n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/identical-matrices1042/1) |
| 6 | Addition of Two Matrices | 🟢 Easy | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/addition-of-two-square-matrices4916/1) |
| 7 | Convert from Any Base to Decimal | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/convert-from-any-base-to-decimal3736/1) |
| 8 | Celsius to Fahrenheit Conversion | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/celsius-to-fahrenheit-conversion5212/1) |
| 9 | Print 1 to N Without Using Loops | 🟢 Easy | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/print-1-to-n-without-using-loops3621/1) |
| 10 | Middle of Three Numbers | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/middle-of-three2926/1) |
| 11 | Greatest of Three Numbers | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/greatest-of-three-numbers2520/1) |
| 12 | Number of Open Doors | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/number-of-open-doors1552/1) |
| 13 | Maximum Possible Sum of Products | 🟢 Easy | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/maximum-possible-sum-of-products3637/1) |
| 14 | Check if Four Points Form a Square | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/check-if-given-four-points-form-a-square3026/1) |
| 15 | Overlapping Rectangles | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/overlapping-rectangles1924/1) |
| 16 | Sum of All Prime Numbers Between 1 and N | 🟢 Easy | O(n log log n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/sum-of-all-prime-numbers-between-1-and-n4404/1) |
| 17 | Check if Number is Power of Another Number | 🟢 Easy | O(log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/check-if-a-number-is-power-of-another-number5442/1) |
| 18 | Common Divisors of Two Numbers | 🟢 Easy | O(√g) | O(d) | [Practice](https://www.geeksforgeeks.org/problems/common-divisors4712/1) |
| 19 | Perfect Number | 🟢 Easy | O(√n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/perfect-number3759/1) |
| 20 | Sum Palindrome (Reverse and Add) | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/sum-palindrome3857/1) |
| 21 | Check if Date Is Valid | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/check-date-valid-or-not/1) |
| 22 | The Lazy Caterer's Problem | 🟢 Easy | O(1) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/the-lazy-caterers-problem2527/1) |
| 23 | Print Sum Triangle for a Given Array | 🟢 Easy | O(n²) | O(n²) | [Practice](https://www.geeksforgeeks.org/problems/sum-triangle-for-given-array1159/1) |
| 24 | Form Largest Number from Digits | 🟢 Easy | O(n log n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/form-largest-number-from-digits5430/1) |
| 25 | Print the Left Element (Alt Min/Max Removal) | 🟢 Easy | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/print-the-left-element2009/1) |
| 26 | Tidy Number | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/tidy-number0519/1) |
| 27 | Mean of Array | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/mean0021/1) |
| 28 | Check if String is Rotated by Two Places | 🟢 Easy | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/check-if-string-is-rotated-by-two-places-1587115620/1) |
| 29 | Binary Representation of a Number | 🟢 Easy | O(log n) | O(log n) | [Practice](https://www.geeksforgeeks.org/problems/binary-representation5003/1) |

---

### P1-1. Count Digits in a Number
**Pattern:** Math | **Key Idea:** Divide by 10 repeatedly and count steps.

```java
public int countDigits(int n) {
    if (n == 0) return 1;
    int count = 0;
    n = Math.abs(n);
    while (n > 0) {
        count++;
        n /= 10;
    }
    return count;
    // Alt one-liner: return (int) Math.log10(n) + 1;
}
// Time: O(d)  Space: O(1)
```

---

### P1-2. Print First N Fibonacci Numbers
**Pattern:** Iteration | **Key Idea:** Track prev two numbers, update each step. Never use plain recursion — it's O(2^n).

```java
public void printFibonacci(int n) {
    int a = 0, b = 1;
    System.out.print(a + " " + b + " ");
    for (int i = 2; i < n; i++) {
        int c = a + b;
        System.out.print(c + " ");
        a = b;
        b = c;
    }
}
// Time: O(n)  Space: O(1)

  class Solution {
    public static int[] fibonacciNumbers(int n) {
        if (n == 0) return new int[0];

        int[] res = new int[n];
        res[0] = 0;

        if (n > 1) res[1] = 1;

        for (int i = 2; i < n; i++) {
            res[i] = res[i - 1] + res[i - 2];
        }

        return res;
    }
}

class Solution {
    public static int[] fibonacciNumbers(int n) {
        int[] res = new int[n];
        for (int i = 0; i < n; i++) {
            res[i] = fib(i);
        }
        return res;
    }

    private static int fib(int n) {
        if (n <= 1) return n;
        return fib(n - 1) + fib(n - 2);
    }
}

class Solution {
    public static int[] fibonacciNumbers(int n) {
        int[] res = new int[n];
        int[] dp = new int[n];
        Arrays.fill(dp, -1);

        for (int i = 0; i < n; i++) {
            res[i] = fib(i, dp);
        }

        return res;
    }

    private static int fib(int n, int[] dp) {
        if (n <= 1) return n;

        if (dp[n] != -1) return dp[n];

        return dp[n] = fib(n - 1, dp) + fib(n - 2, dp);
    }
}
```


---

### P1-3. Program for Armstrong Numbers
**Pattern:** Math | **Key Idea:** Sum of each digit raised to power (number of digits). Compare with original.

```java
public boolean isArmstrong(int n) {
    int original = n;
    int digits = String.valueOf(n).length();
    int sum = 0;
    while (n > 0) {
        int d = n % 10;
        sum += (int) Math.pow(d, digits);
        n /= 10;
    }
    return sum == original;
}
// Time: O(d)  Space: O(1)
```

---

### P1-4. Area of Rectangle, Right Triangle and Circle
**Pattern:** Math | **Key Idea:** Direct formula application.

```java
public void areas(double l, double w, double base, double height, double r) {
    double rect   = l * w;
    double tri    = 0.5 * base * height;
    double circle = Math.PI * r * r;
    System.out.printf("Rect=%.2f  Triangle=%.2f  Circle=%.2f%n", rect, tri, circle);
}

    static int[] getAreas(int L, int W, int B, int H, int R) {
        // code here
        int ans[] = new int[3];
 
        //area of rectangle
        ans[0] = L * W;
        
        //area of right angled triangle
        ans[1] = (int) (0.5 * B * H) ;
        
        //area of circle
        ans[2] = (int) (3.14 * R * R);
        
        return ans;
    }
// Time: O(1)  Space: O(1)
```

---

### P1-5. Check if Two Matrices are Identical
**Pattern:** Brute Force | **Key Idea:** Compare element by element, return false on first mismatch.

```java
public boolean areIdentical(int[][] A, int[][] B) {
    if (A.length != B.length || A[0].length != B[0].length) return false;
    for (int i = 0; i < A.length; i++)
        for (int j = 0; j < A[0].length; j++)
            if (A[i][j] != B[i][j]) return false;
    return true;
}

    int areMatricesIdentical(int N, int[][] Grid1, int[][] Grid2) {
        // code here
        for(int i=0;i<N;i++){
            for(int j=0;j<N;j++){
                if(Grid1[i][j] != Grid2[i][j]){
                    return 0;
                }
            }
        }
        return 1;
    }
// Time: O(m×n)  Space: O(1)
```

---

### P1-6. Addition of Two Matrices
**Pattern:** Math | **Key Idea:** Add corresponding elements.

```java
public int[][] addMatrices(int[][] A, int[][] B) {
    int m = A.length, n = A[0].length;
    int[][] C = new int[m][n];
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            C[i][j] = A[i][j] + B[i][j];
    return C;
}
// Time: O(m×n)  Space: O(m×n)

public void Addition(int[][] matrixA, int[][] matrixB) {
        for(int i=0;i<matrixA.length; i++){
            for(int j=0;j<matrixA[i].length;j++){
                matrixA[i][j] += matrixB[i][j];
            }
        }
    }
```

---

### P1-7. Convert from Any Base to Decimal
**Pattern:** Math | **Key Idea:** Multiply each digit by base^position (right to left).

```java
 static int decimalEquivalent(String N, int b) {
        long res = 0;   // use long to avoid overflow
        long power = 1;

        for (int i = N.length() - 1; i >= 0; i--) {
            char ch = N.charAt(i);
            int digit;

            if (Character.isDigit(ch)) {
                digit = ch - '0';
            } else if (Character.isUpperCase(ch)) {
                digit = ch - 'A' + 10;
            } else {
                digit = ch - 'a' + 10;  // handle lowercase
            }

            // ❗ invalid digit check
            if (digit >= b) return -1;

            res += digit * power;
            power *= b;
        }

        return (int) res;
    }

  class Solution {
    static int decimalEquivalent(String N, int b) {
        try {
            return Integer.parseInt(N, b);
        } catch (NumberFormatException e) {
            return -1; // invalid case
        }
    }
}    
    
public int toDecimal(String num, int base) {
    int result = 0, power = 1;
    for (int i = num.length() - 1; i >= 0; i--) {
        int digit = Character.isDigit(num.charAt(i))
                  ? num.charAt(i) - '0'
                  : num.charAt(i) - 'A' + 10;
        result += digit * power;
        power  *= base;
    }
    return result;
}
// Time: O(d)  Space: O(1)
```

---

### P1-7.2. Convert from Decimal to Any Base 
**Pattern:** Math | **Key Idea:** Multiply each digit by base^position (right to left).

```java
 class Solution {
    static String convertToBase(int N, int base) {
        if (N == 0) return "0";

        StringBuilder sb = new StringBuilder();

        while (N > 0) {
            int rem = N % base;

            if (rem < 10) {
                sb.append(rem);
            } else {
                sb.append((char) ('A' + rem - 10));
            }

            N /= base;
        }

        return sb.reverse().toString();
    }
}

class Solution {
    static String convertToBase(int N, int base) {
        return Integer.toString(N, base).toUpperCase();
    }
}
// Time: O(log₍b₎ N)  Space: O(log₍b₎ N)
```

---

### P1-8. Celsius to Fahrenheit Conversion
**Pattern:** Math | **Key Idea:** F = (C × 9/5) + 32

```java
public double celsiusToFahrenheit(double c) {
    return (c * 9.0 / 5.0) + 32;
}
// Time: O(1)  Space: O(1)
```

---

### P1-9. Print 1 to N Without Using Loops
**Pattern:** Recursion | **Key Idea:** Recurse with (n-1) first, then print n → gives ascending order.

```java
public void print1ToN(int n) {
    if (n == 0) return;
    print1ToN(n - 1);         // go down first
    System.out.print(n + " "); // print on way back up
}
// Time: O(n)  Space: O(n) stack
```

---

### P1-10. Middle of Three Numbers
**Pattern:** Math | **Key Idea:** a + b + c - max - min = middle. No sorting needed.

```java
public int middleOf3(int a, int b, int c) {
    return a + b + c
           - Math.max(a, Math.max(b, c))
           - Math.min(a, Math.min(b, c));
}
// Time: O(1)  Space: O(1)
```

---

### P1-11. Greatest of Three Numbers
**Pattern:** Math | **Key Idea:** Chained Math.max.

```java
public int greatest(int a, int b, int c) {
    return Math.max(a, Math.max(b, c));
}
// Time: O(1)  Space: O(1)
```

---

### P1-12. Number of Open Doors
**Pattern:** Math / Pattern Recognition | **Key Idea:** Door i is toggled by every divisor. Odd number of divisors → open. Only perfect squares have odd divisors.
Each door is toggled as many times as its number of divisors. Only perfect squares have an odd number of divisors, so the number of open doors is equal to the count of perfect squares up to n, i.e., floor(√n).

```java
public int openDoors(int n) {
    // Count of perfect squares ≤ n = count of open doors
    return (int) Math.sqrt(n);
}
// Time: O(1)  Space: O(1)
```

---

### P1-13. Maximum Possible Sum of Products
**Pattern:** Greedy + Sorting | **Key Idea:** Sort both arrays. Pair largest with largest to maximize sum.

```java
public long maxSumProducts(int[] a, int[] b) {
    Arrays.sort(a);
    Arrays.sort(b);
    long sum = 0;
    for (int i = 0; i < a.length; i++)
        sum += (long) a[i] * b[i];
    return sum;
}
// Time: O(n log n)  Space: O(1)
```

---

### P1-14. Check if Four Points Form a Square
**Pattern:** Geometry | **Key Idea:** Compute all 6 pairwise distances². A square has 4 equal sides + 2 equal (longer) diagonals, no zero distance.

```java
class Solution {
    int fourPointSquare(int points[][]) {
        // code here
        int p1[] = points[0];
        int p2[] = points[1];
        int p3[] = points[2];
        int p4[] = points[3];
        
        int [] d = {
            dist(p1,p2), dist(p1,p3), dist(p1,p4),
            dist(p2,p3), dist(p2,p4), dist(p3,p4)
        };
        
        Arrays.sort(d);
        
        int res = ( d[0] > 0
            && d[0] == d[1] && d[1] == d[2] && d[2] == d[3]
            && d[4] == d[5]) ? 1 : 0;
            
        return res;
        
    }
    
    private int dist(int a[], int b[]){
        return (a[0]-b[0]) * (a[0] - b[0]) + (a[1] -b[1]) * (a[1] - b[1]);
    }
};

public boolean isSquare(int[] p1, int[] p2, int[] p3, int[] p4) {
    int[] d = {
        dist(p1,p2), dist(p1,p3), dist(p1,p4),
        dist(p2,p3), dist(p2,p4), dist(p3,p4)
    };
    Arrays.sort(d);
    // 4 equal sides [0..3], 2 equal diagonals [4..5], no zero
    return d[0] > 0
        && d[0] == d[1] && d[1] == d[2] && d[2] == d[3]
        && d[4] == d[5];
}
private int dist(int[] a, int[] b) {
    return (a[0]-b[0])*(a[0]-b[0]) + (a[1]-b[1])*(a[1]-b[1]);
}
// Time: O(1)  Space: O(1)
```

---

### P1-15. Overlapping Rectangles
**Pattern:** Geometry | **Key Idea:** They DON'T overlap if one is completely left/right/above/below the other.

```java
1. Ek rectangle completely left me ho
R1.x < L2.x   OR   R2.x < L1.x
2. Ek rectangle completely upar ho
R1.y > L2.y   OR   R2.y > L1.y
class Solution {
    int doOverlap(int L1[], int R1[], int L2[], int R2[]) {
        
        // Check horizontal separation
        if (R1[0] < L2[0] || R2[0] < L1[0]) {
            return 0;
        }
        
        // Check vertical separation
        if (R1[1] > L2[1] || R2[1] > L1[1]) {
            return 0;
        }
        
        return 1; // Overlap
    }
}
// Rectangle: (x1,y1) = bottom-left, (x2,y2) = top-right
public boolean doOverlap(int x1, int y1, int x2, int y2,
                         int x3, int y3, int x4, int y4) {
    if (x1 >= x4 || x3 >= x2) return false; // one is to the left
    if (y1 >= y4 || y3 >= y2) return false; // one is above
    return true;
}
// Time: O(1)  Space: O(1)
```

---

### P1-16. Sum of All Prime Numbers Between 1 and N
**Pattern:** Sieve of Eratosthenes | **Key Idea:** Mark all composites, then sum remaining primes.

```java
class Solution {
    public int prime_Sum(int n) {
        
        boolean[] isPrime = new boolean[n + 1];
        
        // Step 1: sabko prime maan lo
        for(int i = 2; i <= n; i++){
            isPrime[i] = true;
        }
        
        // Step 2: multiples hatao
        for(int i = 2; i * i <= n; i++){
            if(isPrime[i]){
                for(int j = i * i; j <= n; j += i){
                    isPrime[j] = false;
                }
            }
        }
        
        // Step 3: sum nikaalo
        int sum = 0;
        for(int i = 2; i <= n; i++){
            if(isPrime[i]){
                sum += i;
            }
        }
        
        return sum;
    }
}

class Solution {
    // Method to calculate the sum of prime numbers up to a given value
    public int prime_Sum(int n) {
        int sum = 0;
        // Loop through numbers up to n
        for (int i = 1; i <= n; i++) {
            // Check if the number is prime
            boolean flag = isPrime(i);
            if (flag == true) sum = sum + i;
        }
        return sum;
    }

    // Method to check if a number is prime
    static boolean isPrime(int n) {
        // Corner case: 1 and negative numbers are not prime
        if (n <= 1) return false;

        // Check from 2 to square root of n
        for (int i = 2; i <= Math.sqrt(n); i++)

            // If n is divisible by any number other than 1 and itself, it's not prime
            if (n % i == 0) return false;

        return true;
    }
}

public long sumPrimes(int n) {
    boolean[] isComposite = new boolean[n + 1];
    long sum = 0;
    for (int i = 2; i <= n; i++) {
        if (!isComposite[i]) {
            sum += i;
            for (int j = 2 * i; j <= n; j += i)
                isComposite[j] = true;
        }
    }
    return sum;
}
// Time: O(n log log n)  Space: O(n)
```

---

### P1-17. Check if Number is Power of Another Number
**Pattern:** Math | **Key Idea:** Multiply base repeatedly. If result == n at any point → yes.

```java
class Solution {
    public boolean isPower(int x, int y) {
        
        // Edge case: y = 1 → always true (x^0 = 1)
        if (y == 1) return true;
        
        // Edge case: x = 1
        if (x == 1) return y == 1;
        
        // Divide y repeatedly
        while (y % x == 0) {
            y /= x;
        }
        
        return y == 1;
    }
}

class Solution {
    public boolean isPower(int x, int y) {
        
        // Edge case: 1^k = 1 only
        if (x == 1) return y == 1;

        // Edge case: x^0 = 1
        if (y == 1) return true;

        // Compute logarithm
        double res = Math.log(y) / Math.log(x);

        // Compare with rounded value using a small
        // tolerance to avoid floating point errors
        return Math.abs(res - Math.round(res)) < 1e-10;
    }
}

public boolean isPower(int n, int base) {
    if (base == 1) return n == 1;
    long curr = base;
    while (curr < n) curr *= base;
    return curr == n;
}
// Time: O(log_base(n))  Space: O(1)
```

---

### P1-18. Common Divisors of Two Numbers
**Pattern:** Math / GCD | **Key Idea:** GCD(a,b) contains all common divisors. Find all divisors of GCD.

```java
👉 Common divisors of a and b =
👉 Divisors of GCD(a, b)
class Solution {
    public int commDiv(int a, int b) {
        
        int g = gcd(a, b);
        int count = 0;
        
        for(int i = 1; i * i <= g; i++){
            if(g % i == 0){
                
                if(i * i == g){
                    count += 1; // perfect square case
                } else {
                    count += 2; // pair (i, g/i)
                }
            }
        }
        
        return count;
    }
    
    private int gcd(int a, int b){
        while(b != 0){
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}

public List<Integer> commonDivisors(int a, int b) {
    int g = gcd(a, b);
    List<Integer> result = new ArrayList<>();
    for (int i = 1; i * i <= g; i++) {
        if (g % i == 0) {
            result.add(i);
            if (i != g / i) result.add(g / i);
        }
    }
    return result;
}
private int gcd(int a, int b) {
    return b == 0 ? a : gcd(b, a % b);
}
// Time: O(√g)  Space: O(d)
```

---
### P1-19. Perfect Number
**Pattern:** Math | **Key Idea:** sum of factorial of its digit is equal to the given number.

```java
// Back-end complete function Template for Java

class Solution {
    int isPerfect(int N) {
        // Array to store factorials.
        int fact[] = new int[10];
        fact[0] = 1;
        for (int i = 1; i < 10; i++) fact[i] = fact[i - 1] * i;
        // storing the factorial of all digits
        // makes sure we don't calculate factorial
        // for digits multiple times.
        int store = N; // storing original number
        int sum = 0;
        while (N > 0) {
            sum += fact[N % 10]; // adding factorials of digits
            N /= 10;
        }
        return (store == sum ? 1 : 0);
    }
}
```

---
### P1-19-2. Perfect Number
**Pattern:** Math | **Key Idea:** Sum of all proper divisors (1 to n-1) == n. Use √n loop.

```java
public boolean isPerfect(int n) {
    if (n <= 1) return false;
    int sum = 1; // 1 is always a proper divisor
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            if (i != n / i) sum += n / i;
        }
    }
    return sum == n;
}
// Time: O(√n)  Space: O(1)
```

---

### P1-20. Sum Palindrome (Reverse and Add)
**Pattern:** Math | **Key Idea:** n + reverse(n) should itself be a palindrome.

```java
// User function Template for Java
class Solution {
     // Function to find palindrome by adding reverse of the number to itself.

    static int isSumPalindrome(int n) {
        // code here
        int itr = 0;
        
        while(!isPalindrome(n) && itr<5 ){
            int rev = reverse(n);
            n += rev;
            itr++;
        }
        
         if(isPalindrome(n)){
            return n;
         }
        return -1;
    }
    
    // Function to reverse the digits of a number.
    private static int reverse(int n){
        int sum = 0;
        while(n!=0){
            sum = sum *10 + n%10;
            n/=10;
        }
        return sum;
    }
    
     /* Function to check whether the number is palindrome or not */
    private static boolean isPalindrome(int n){
       return reverse(n) == n;
    }
}
public boolean isSumPalindrome(int n) {
    int reversed = reverse(n);
    int sum = n + reversed;
    return sum == reverse(sum);
}
private int reverse(int n) {
    int rev = 0;
    while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
    return rev;
}
// Time: O(d)  Space: O(1)
```

---

### P1-21. Check if Date Is Valid
**Pattern:** Math / Conditionals | **Key Idea:** Validate month, then day based on days-in-month array. Handle leap year for Feb.

```java
class Solution {
    
    static int isValidDate(int d, int m, int y) {
        
        // Check valid year range
        if (y < 1800 || y > 9999) return 0;
        
        // Check valid month and day
        if (m < 1 || m > 12 || d < 1) return 0;
        
        int[] days = {31,28,31,30,31,30,31,31,30,31,30,31};
        
        // Leap year check for February
        if (m == 2 && isLeapYear(y)) {
            return d <= 29 ? 1 : 0;
        }
        
        return d <= days[m - 1] ? 1 : 0;
    }
    
    private static boolean isLeapYear(int y) {
        return (y % 4 == 0 && y % 100 != 0) || (y % 400 == 0);
    }
}

public boolean isValidDate(int d, int m, int y) {
    if (y < 1 || m < 1 || m > 12 || d < 1) return false;
    int[] days = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    if (isLeap(y)) days[1] = 29;
    return d <= days[m - 1];
}
private boolean isLeap(int y) {
    return (y % 4 == 0 && y % 100 != 0) || (y % 400 == 0);
}
// Time: O(1)  Space: O(1)
```

---

### P1-22. The Lazy Caterer's Problem
**Pattern:** Math Formula | **Key Idea:** Max pieces with n cuts = n*(n+1)/2 + 1

```java
public int lazyCaterer(int n) {
    return n * (n + 1) / 2 + 1;
}
// Time: O(1)  Space: O(1)
```

---

### P1-23. Print Sum Triangle for a Given Array
**Pattern:** Simulation | **Key Idea:** Each new row = sum of adjacent elements of previous row. Build bottom-up.

```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    static final int MOD = 1000000007;
    public ArrayList<Integer> getTriangle(int[] arr) {
        ArrayList<Integer> ans = new ArrayList<>();
        List<Integer> curr = Arrays.stream(arr).boxed().collect(Collectors.toList());
        ans.addAll(curr);

        while(curr.size()>1){
            List<Integer> temp = new ArrayList<>();
            for(int i=1;i<curr.size();i++){
                int sum = (curr.get(i) + curr.get(i-1)) % MOD;
                temp.add(sum);
            }
            curr = temp;
            ans.addAll(0,curr);
        }

        return ans;
    }
}

public void printSumTriangle(int[] arr) {
    List<int[]> triangle = new ArrayList<>();
    triangle.add(arr.clone());
    while (arr.length > 1) {
        int[] next = new int[arr.length - 1];
        for (int i = 0; i < arr.length - 1; i++)
            next[i] = arr[i] + arr[i + 1];
        triangle.add(0, next); // prepend
        arr = next;
    }
    for (int[] row : triangle)
        System.out.println(Arrays.toString(row));
}
// Time: O(n²)  Space: O(n²)
```

---

### P1-24. Form Largest Number from Digits
**Pattern:** Greedy | **Key Idea:** Sort digits in descending order, concatenate.

```java
class Solution {
    // Function to find the maximum number by sorting the array in descending order
    public String MaxNumber(int arr[]) {
        StringBuilder s = new StringBuilder();
        int n = arr.length;
        // Array to store the count of each digit in the input array
        int[] h = new int[10]; // Range is 0-9, so array size is 10

        // Counting the occurrence of each digit
        for (int i = 0; i < n; i++) {
            // Incrementing the count of digit a[i] in array h
            h[arr[i]]++;
        }

        // Building the maximum number by looping through the digits in descending order
        for (int i = 9; i >= 0; i--) {
            while (h[i]-- > 0) {
                s.append(i);
            }
        }
        // Returning the maximum number as a string
        return s.toString();
    }
}


class Solution {
    public String largestNumber(int[] arr) {
        int n = arr.length;
        String nums[] = new String[n];

        for(int i = 0; i<n; i++){
            nums[i] = String.valueOf(arr[i]);
        }

        Arrays.sort(nums, (a,b)-> (b+a).compareTo(a+b));
        // handle all zeros case
        if(nums[0].equals("0")) {
            return "0";
        }
        StringBuilder sb = new StringBuilder();
        for(String str: nums){
            sb.append(str);
        }

        return sb.toString();
    }
}
class Solution {

    public String MaxNumber(int arr[]) {
        // code here.
        Arrays.sort(arr);
        StringBuilder sb = new StringBuilder();
        
        for(int i=arr.length-1; i>=0; i--){
            sb.append(arr[i]);
        }
        
        return sb.toString();
    }
}

class Solution {
    public int triangularSum(int[] nums) {
        int n = nums.length;

        while(n>1){
            for(int i=0;i<n-1;i++){
                nums[i] = (nums[i] + nums[i+1]) % 10;
            }
            n--;
        }
        return nums[0];
    }
}

class Solution {
    public ArrayList<Integer> getTriangle(int[] arr) {
        int n = arr.length;
        // Initialize a 2D array to store the triangle
        int[][] tri = new int[n][n];

        // Initialize the last row of the triangle
        for (int i = 0; i < n; i++) {
            tri[n - 1][i] = arr[i];
        }

        // Fill other rows
        for (int i = n - 2; i >= 0; i--) {
            for (int j = 0; j <= i; j++) {
                tri[i][j] = (tri[i + 1][j] + tri[i + 1][j + 1]) % 1000000007;
            }
        }

        // Storing the triangle in an ArrayList
        ArrayList<Integer> Triangle = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                Triangle.add((int)tri[i][j]);
            }
        }

        return Triangle;
    }
}
public String formLargest(int[] digits) {
    Integer[] arr = new Integer[digits.length];
    for (int i = 0; i < digits.length; i++) arr[i] = digits[i];
    Arrays.sort(arr, (a, b) -> b - a);
    StringBuilder sb = new StringBuilder();
    for (int d : arr) sb.append(d);
    return sb.toString();
}
// Time: O(n log n)  Space: O(n)
```

---

### P1-25. Print the Left Element (Alternate Min/Max Removal)
**Pattern:** Sorting + Simulation | **Key Idea:** Sort. Alternate remove min (advance lo) then max (reduce hi). Last standing is answer.

```java
class Solution {
    public static int leftElement(int[] arr) {
        // code here
        
        Arrays.sort(arr);
        int n = arr.length;
        if(n%2==0){
            n = n/2 - 1;
        }else{
            n = n /2;
        }
        
        return arr[n];
        
    }
}

public int printLeft(int[] arr) {
    Arrays.sort(arr);
    int lo = 0, hi = arr.length - 1;
    boolean removeMin = true;
    while (lo < hi) {
        if (removeMin) lo++;
        else hi--;
        removeMin = !removeMin;
    }
    return arr[lo];
}
// Time: O(n log n)  Space: O(1)
```

---

### P1-26. Tidy Number
**Pattern:** Math | **Key Idea:** Digits must be non-decreasing left to right. Check each pair.

```java
class Solution {
    int isTidy(int N) {
        // To store previous digit (Assigning
        // initial value which is more than any
        // digit)
        int prev = 10;

        // Traverse all digits from right to
        // left and check if any digit is
        // smaller than previous.
        while (N > 0) {
            int rem = N % 10;
            N /= 10;
            if (rem > prev) return 0;
            prev = rem;
        }
        return 1;
    }
}

public boolean isTidy(int n) {
    String s = String.valueOf(n);
    for (int i = 1; i < s.length(); i++)
        if (s.charAt(i) < s.charAt(i - 1)) return false;
    return true;
}
// Time: O(d)  Space: O(d)
```

---

### P1-27. Mean of Array
**Pattern:** Math | **Key Idea:** Sum all elements, divide by count.

```java
class Solution {
    public static int findMean(int[] arr) {
        int sum = 0;
        int n = arr.length;
        for (int i = 0; i < n; i++)
            sum += arr[i]; // First, the Sum of the Array is Calculated

        int ans = sum / n; // The Sum is divided with N to get it's Mean.

        return ans;
    }
};

public double mean(int[] arr) {
    long sum = 0;
    for (int x : arr) sum += x;
    return (double) sum / arr.length;
}
// Time: O(n)  Space: O(1)
```

---

### P1-28. Check if String is Rotated by Two Places
**Pattern:** String | **Key Idea:** Two cases — left rotate by 2, or right rotate by 2. Compare both.

```java
class Solution {
    // Function to check if a string can be obtained by rotating another string by
    // exactly 2 places
    static boolean isRotated(String s1, String s2) {
        if (s1.length() != s2.length()) return false;

        if (s1.length() <= 2 || s2.length() <= 2) return s1.equals(s2);

        int len = s2.length();

        // Storing anti-clockwise rotation of string
        String anticlockRot = s2.substring(len - 2) + s2.substring(0, len - 2);

        // Storing clockwise rotation of string
        String clockRot = s2.substring(2) + s2.substring(0, 2);

        // Checking if any of them is equal to s1
        return s1.equals(clockRot) || s1.equals(anticlockRot);
    }
}

public boolean isRotatedBy2(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    int n = s1.length();
    String leftRot  = s1.substring(2) + s1.substring(0, 2);
    String rightRot = s1.substring(n - 2) + s1.substring(0, n - 2);
    return s2.equals(leftRot) || s2.equals(rightRot);
}
// Time: O(n)  Space: O(n)
```

---

### P1-29. Binary Representation of a Number
**Pattern:** Bit Manipulation | **Key Idea:** Extract LSB with n & 1, prepend to result, right-shift n.

```java
class Solution {
    static String getBinary(int n) {
        return String.format("%32s", Integer.toBinaryString(n))
                     .replace(' ', '0');
    }
}

class Solution {
    public String getBinaryRep(int n) {
        StringBuilder ans = new StringBuilder();

        for (int i = 31; i >= 0; i--) {
            int bit = (n >> i) & 1;
            ans.append(bit);
        }

        return ans.toString();
    }
}

public String toBinaryString(int n) {
    if (n == 0) return "0";
    StringBuilder sb = new StringBuilder();
    while (n > 0) {
        sb.insert(0, n & 1);
        n >>= 1;
    }
    return sb.toString();
    // Alt: Integer.toBinaryString(n)
}
// Time: O(log n)  Space: O(log n)
```

---

---

## Pattern 2 — Two Pointers (6 problems)

> **When to use:** Sorted array + find pair/triplet, in-place modification, palindrome check.  
> **Core rule:** `sum < target → L++` | `sum > target → R--` | `sum == target → found ✅`

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 30 | Pair with Given Sum (Two Sum) | 🟢 Easy | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/count-pairs-with-given-sum5022/1) |
| 31 | Remove Duplicates from Sorted Array | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/remove-duplicate-elements-from-sorted-array/1) |
| 32 | Merge Two Sorted Arrays Without Extra Space | 🟡 Medium | O(m+n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1) |
| 33 | Sentence Palindrome | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/string-palindromic-ignoring-spaces4723/1) |
| 34 | Reverse a String | 🟢 Easy | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/reverse-a-string/1) |
| 35 | Next Permutation | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/next-permutation5226/1) |

---

### P2-30. Pair with Given Sum (Two Sum)
**Pattern:** Two Pointers (Both Ends) | **Key Idea:** Sort first. L=0, R=n-1. Move based on sum vs target.

```java
public int[] twoSum(int[] nums, int target) {
    Arrays.sort(nums);
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if      (sum == target) return new int[]{left, right};
        else if (sum < target)  left++;
        else                    right--;
    }
    return new int[]{-1};
}
// Time: O(n log n)  Space: O(1)
```

---

### P2-31. Remove Duplicates from Sorted Array
**Pattern:** Slow/Fast Pointer | **Key Idea:** Fast reads always. Slow writes only when new unique value found.

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int slow = 0;
    for (int fast = 1; fast < nums.length; fast++)
        if (nums[fast] != nums[slow])
            nums[++slow] = nums[fast];
    return slow + 1; // new length
}
// Time: O(n)  Space: O(1)
```

---

### P2-32. Merge Two Sorted Arrays Without Extra Space
**Pattern:** Two Pointers (Reverse merge) | **Key Idea:** Merge from the end. Compare from back of each, place largest at rightmost slot.

```java
public void merge(int[] arr1, int m, int[] arr2, int n) {
    int i = m - 1, j = n - 1, k = m + n - 1;
    while (i >= 0 && j >= 0)
        arr1[k--] = (arr1[i] > arr2[j]) ? arr1[i--] : arr2[j--];
    while (j >= 0) arr1[k--] = arr2[j--]; // remaining of arr2
}
// Time: O(m+n)  Space: O(1)
```

---

### P2-33. Sentence Palindrome (Valid Palindrome)
**Pattern:** Two Pointers (Both Ends) | **Key Idea:** Skip non-alphanumeric. Compare lowercase chars. Move L and R inward.

```java
public boolean isPalindrome(String s) {
    int l = 0, r = s.length() - 1;
    while (l < r) {
        while (l < r && !Character.isLetterOrDigit(s.charAt(l))) l++;
        while (l < r && !Character.isLetterOrDigit(s.charAt(r))) r--;
        if (Character.toLowerCase(s.charAt(l)) !=
            Character.toLowerCase(s.charAt(r))) return false;
        l++; r--;
    }
    return true;
}
// Time: O(n)  Space: O(1)
```

---

### P2-34. Reverse a String
**Pattern:** Two Pointers (Both Ends) | **Key Idea:** Swap arr[L] and arr[R], move both inward until they meet.

```java
public String reverseString(String s) {
    char[] arr = s.toCharArray();
    int l = 0, r = arr.length - 1;
    while (l < r) {
        char t = arr[l]; arr[l++] = arr[r]; arr[r--] = t;
    }
    return new String(arr);
}
// Time: O(n)  Space: O(n)
```

---

### P2-35. Next Permutation
**Pattern:** Two Pointers | **Key Idea:** 4 steps — find pivot → find successor → swap → reverse suffix.

```java
public void nextPermutation(int[] nums) {
    int n = nums.length, i = n - 2;
    // Step 1: find rightmost i where nums[i] < nums[i+1]
    while (i >= 0 && nums[i] >= nums[i + 1]) i--;
    if (i >= 0) {
        // Step 2: find rightmost j > i where nums[j] > nums[i]
        int j = n - 1;
        while (nums[j] <= nums[i]) j--;
        // Step 3: swap
        int tmp = nums[i]; nums[i] = nums[j]; nums[j] = tmp;
    }
    // Step 4: reverse from i+1 to end
    int l = i + 1, r = n - 1;
    while (l < r) {
        int t = nums[l]; nums[l++] = nums[r]; nums[r--] = t;
    }
}
// Time: O(n)  Space: O(1)
```

---

---

## Pattern 3 — Bit Manipulation (2 problems)

> **When to use:** XOR tricks, toggle bits, find lone element.  
> **Core rules:** `a ^ a = 0` | `a ^ 0 = a` | XOR is commutative and associative

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 36 | Party of Couples (Find Lone Person) | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/alone-in-couple5507/1) |
| 37 | Find All Distinct Subset Sums | 🔴 Hard | O(n·2ⁿ) | O(2ⁿ) | [Practice](https://www.geeksforgeeks.org/problems/find-all-distinct-subset-or-subsequence-sums4424/1) |

---

### P3-36. Party of Couples (Find Lone Person)
**Pattern:** XOR | **Key Idea:** XOR all elements. Pairs cancel out (a^a=0). What remains is the lone element.

```java
public int findLone(int[] arr) {
    int result = 0;
    for (int x : arr) result ^= x;
    return result;
}
// Time: O(n)  Space: O(1)
```

---

### P3-37. Find All Distinct Subset / Subsequence Sums
**Pattern:** Sorting + DP Set | **Key Idea:** Sort first (to handle duplicates). Use DP set tracking all reachable sums.

```java
public List<Integer> distinctSubsetSums(int[] arr) {
    Arrays.sort(arr);
    Set<Integer> dp = new TreeSet<>();
    dp.add(0);
    for (int num : arr) {
        Set<Integer> next = new TreeSet<>(dp);
        for (int s : dp) next.add(s + num);
        dp = next;
    }
    return new ArrayList<>(dp);
}
// Time: O(n·2ⁿ) worst case  Space: O(2ⁿ)
```

---

---

## Pattern 4 — Sorting / Greedy (7 problems)

> **When to use:** Optimal choice at each step. Usually requires sorting first.  
> **Key insight:** Greedy works when local optimal = global optimal.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 38 | Minimum Platforms Required | 🟡 Medium | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1) |
| 39 | Job Sequencing Problem | 🟡 Medium | O(n log n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1) |
| 40 | Largest Number Formed from an Array | 🟡 Medium | O(n log n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/largest-number-formed-from-an-array1117/1) |
| 41 | Minimum Number of Jumps | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/minimum-number-of-jumps-1587115620/1) |
| 42 | Minimize the Heights II | 🟡 Medium | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/minimize-the-heights3351/1) |
| 43 | Rotate Array | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/rotate-array-by-n-elements-1587115621/1) |
| 44 | Sort String of Characters | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/sort-a-string2943/1) |

---

### P4-38. Minimum Platforms Required
**Pattern:** Sorting + Two Pointers | **Key Idea:** Sort arrivals and departures separately. If next train arrives before current departs → need new platform.

```java
public int minPlatforms(int[] arr, int[] dep) {
    Arrays.sort(arr);
    Arrays.sort(dep);
    int platforms = 1, maxPlatforms = 1;
    int i = 1, j = 0;
    while (i < arr.length) {
        if (arr[i] <= dep[j]) { platforms++; i++; }
        else                  { platforms--; j++; }
        maxPlatforms = Math.max(maxPlatforms, platforms);
    }
    return maxPlatforms;
}
// Time: O(n log n)  Space: O(1)
```

---

### P4-39. Job Sequencing Problem
**Pattern:** Greedy (Sort by Profit Desc) | **Key Idea:** Sort by profit desc. For each job, find latest free slot ≤ deadline.

```java
public int[] jobSequencing(int[] deadline, int[] profit) {
    int n = deadline.length;
    Integer[] idx = new Integer[n];
    for (int i = 0; i < n; i++) idx[i] = i;
    Arrays.sort(idx, (a, b) -> profit[b] - profit[a]);
    int maxD = Arrays.stream(deadline).max().getAsInt();
    int[] slots = new int[maxD + 1]; Arrays.fill(slots, -1);
    int count = 0, total = 0;
    for (int i : idx) {
        for (int d = deadline[i]; d > 0; d--) {
            if (slots[d] == -1) {
                slots[d] = i; count++; total += profit[i]; break;
            }
        }
    }
    return new int[]{count, total};
}
// Time: O(n log n + n·maxD)  Space: O(maxD)
```

---

### P4-40. Largest Number Formed from an Array
**Pattern:** Custom Sort | **Key Idea:** Comparator: prefer (b+a) over (a+b) as strings. If "30"+"3" > "3"+"30" → "30" comes first.

```java
public String largestNumber(int[] nums) {
    String[] s = new String[nums.length];
    for (int i = 0; i < nums.length; i++) s[i] = String.valueOf(nums[i]);
    Arrays.sort(s, (a, b) -> (b + a).compareTo(a + b));
    if (s[0].equals("0")) return "0";
    StringBuilder sb = new StringBuilder();
    for (String t : s) sb.append(t);
    return sb.toString();
}
// Time: O(n log n)  Space: O(n)
```

---

### P4-41. Minimum Number of Jumps
**Pattern:** Greedy | **Key Idea:** Track farthest reachable index. When current window exhausted → must jump. Increment jumps.

```java
public int minJumps(int[] nums) {
    int jumps = 0, currEnd = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == currEnd) {
            jumps++;
            currEnd = farthest;
        }
        if (currEnd >= nums.length - 1) break;
    }
    return jumps;
}
// Time: O(n)  Space: O(1)
```

---

### P4-42. Minimize the Heights II
**Pattern:** Sorting + Greedy | **Key Idea:** Sort. For each split i: towers 0..i get +k, towers i+1..n-1 get -k. Track min(max - min).

```java
public int minimizeHeights(int[] arr, int k) {
    int n = arr.length;
    Arrays.sort(arr);
    int result = arr[n - 1] - arr[0]; // no-change baseline
    for (int i = 0; i < n - 1; i++) {
        int maxH = Math.max(arr[i] + k, arr[n - 1] - k);
        int minH = Math.min(arr[0] + k, arr[i + 1] - k);
        if (minH < 0) continue;
        result = Math.min(result, maxH - minH);
    }
    return result;
}
// Time: O(n log n)  Space: O(1)
```

---

### P4-43. Rotate Array
**Pattern:** Reversal Algorithm | **Key Idea:** 3 reverses = 1 rotation. Reverse all → reverse first k → reverse rest. O(1) space.

```java
public void rotate(int[] nums, int k) {
    int n = nums.length;
    k %= n;
    reverse(nums, 0, n - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, n - 1);
}
private void reverse(int[] a, int l, int r) {
    while (l < r) { int t = a[l]; a[l++] = a[r]; a[r--] = t; }
}
// Time: O(n)  Space: O(1)
```

---

### P4-44. Sort String of Characters
**Pattern:** Counting Sort | **Key Idea:** Count frequency of each char (size-26 array). Rebuild string in order.

```java
public String sortString(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 26; i++)
        for (int j = 0; j < freq[i]; j++) sb.append((char)('a' + i));
    return sb.toString();
}
// Time: O(n)  Space: O(1)
```

---

---

## Pattern 5 — Sliding Window / Prefix Sum / Kadane's (4 problems)

> **When to use:** Subarray / contiguous elements with a condition.  
> **Rule:** Expand right always. Shrink left when condition violated.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 45 | Subarray with Given Sum | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1) |
| 46 | Number of Subarrays with Sum = k | 🟡 Medium | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1) |
| 47 | Kadane's Algorithm (Max Subarray Sum) | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/kadanes-algorithm-1587115620/1) |
| 48 | Best Time to Buy and Sell Stock | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/buy-stock-2/1) |

---

### P5-45. Subarray with Given Sum
**Pattern:** Sliding Window (Variable) | **Key Idea:** Expand right. If sum > target shrink from left. Record when sum == target.

```java
public int[] subarrayWithSum(int[] arr, int target) {
    int left = 0, sum = 0;
    for (int right = 0; right < arr.length; right++) {
        sum += arr[right];
        while (sum > target && left <= right) sum -= arr[left++];
        if (sum == target) return new int[]{left + 1, right + 1}; // 1-indexed
    }
    return new int[]{-1};
}
// Time: O(n)  Space: O(1)
```

---

### P5-46. Number of Subarrays with Sum = k
**Pattern:** Prefix Sum + HashMap | **Key Idea:** At each index, check how many prefix sums equal (currSum - k). Those subarrays end at current index.

```java
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1); // empty prefix
    int count = 0, sum = 0;
    for (int num : nums) {
        sum += num;
        count += map.getOrDefault(sum - k, 0);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return count;
}
// Time: O(n)  Space: O(n)
```

---

### P5-47. Kadane's Algorithm — Maximum Subarray Sum
**Pattern:** Kadane's | **Key Idea:** `currSum = max(num, currSum + num)`. Start new subarray if current element alone is better.

```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0], currSum = nums[0];
    for (int i = 1; i < nums.length; i++) {
        currSum = Math.max(nums[i], currSum + nums[i]);
        maxSum  = Math.max(maxSum, currSum);
    }
    return maxSum;
}
// Time: O(n)  Space: O(1)
```

---

### P5-48. Best Time to Buy and Sell Stock
**Pattern:** Prefix Min / Greedy | **Key Idea:** Track minPrice so far. At each step: profit = price - minPrice. Update maxProfit.

```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE, maxProfit = 0;
    for (int price : prices) {
        minPrice  = Math.min(minPrice, price);
        maxProfit = Math.max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
// Time: O(n)  Space: O(1)
```

---

---

## Pattern 6 — HashMap / Frequency (3 problems)

> **When to use:** Counting occurrences, O(1) lookup, finding duplicates/majority.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 49 | Count Frequencies in an Array | 🟢 Easy | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/frequency-of-elements--111353/1) |
| 50 | Majority Element | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/majority-element-1587115620/1) |
| 51 | Remove Common Characters and Concatenate | 🟢 Easy | O(m+n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/remove-common-characters-and-concatenate-1587115621/1) |

---

### P6-49. Count Frequencies in an Array
**Pattern:** HashMap | **Key Idea:** Single pass. Increment count for each element in map.

```java
public void countFrequencies(int[] arr) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int x : arr)
        freq.put(x, freq.getOrDefault(x, 0) + 1);
    freq.forEach((k, v) -> System.out.println(k + " -> " + v));
}
// Time: O(n)  Space: O(n)
```

---

### P6-50. Majority Element (> n/2 times)
**Pattern:** Boyer-Moore Voting | **Key Idea:** Track candidate. If count=0 → new candidate. count++ on match, count-- otherwise. O(1) space!

```java
public int majorityElement(int[] nums) {
    int candidate = nums[0], count = 1;
    for (int i = 1; i < nums.length; i++) {
        if (count == 0)              { candidate = nums[i]; count = 1; }
        else if (nums[i] == candidate) count++;
        else                           count--;
    }
    return candidate; // guaranteed to exist per problem constraints
}
// Time: O(n)  Space: O(1)
```

---

### P6-51. Remove Common Characters and Concatenate
**Pattern:** Set / Frequency Array | **Key Idea:** Find characters common to both strings. Build result from chars NOT in common set.

```java
public String removeCommon(String s1, String s2) {
    Set<Character> common = new HashSet<>();
    for (char c : s1.toCharArray())
        if (s2.indexOf(c) >= 0) common.add(c);
    StringBuilder sb = new StringBuilder();
    for (char c : s1.toCharArray()) if (!common.contains(c)) sb.append(c);
    for (char c : s2.toCharArray()) if (!common.contains(c)) sb.append(c);
    return sb.toString();
}
// Time: O(m+n)  Space: O(1) — at most 26 chars
```

---

---

## Pattern 7 — Binary Search (3 problems)

> **When to use:** Sorted input, or problem where answer has monotone property (feasibility check).  
> **Template:** `mid = lo + (hi - lo) / 2` — always use this to avoid overflow.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 52 | Binary Search | 🟢 Easy | O(log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/binary-search-1587115620/1) |
| 53 | Allocate Minimum Number of Pages | 🟡 Medium | O(n log S) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) |
| 54 | Find the Element Appearing Once in Sorted Array | 🟡 Medium | O(log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/element-appearing-once2552/1) |

---

### P7-52. Binary Search
**Pattern:** Binary Search | **Key Idea:** Standard template. Shrink window based on midpoint comparison.

```java
public int binarySearch(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if      (arr[mid] == target) return mid;
        else if (arr[mid] < target)  lo = mid + 1;
        else                         hi = mid - 1;
    }
    return -1;
}
// Time: O(log n)  Space: O(1)
```

---

### P7-53. Allocate Minimum Number of Pages
**Pattern:** Binary Search on Answer | **Key Idea:** Search space = [max(arr), sum(arr)]. For each mid, check if allocation is feasible with ≤ m students.

```java
public int allocatePages(int[] books, int students) {
    int lo = books[0], hi = 0;
    for (int b : books) { lo = Math.max(lo, b); hi += b; }
    int result = hi;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (feasible(books, students, mid)) { result = mid; hi = mid - 1; }
        else lo = mid + 1;
    }
    return result;
}
private boolean feasible(int[] books, int k, int maxPages) {
    int count = 1, pages = 0;
    for (int b : books) {
        if (pages + b > maxPages) { count++; pages = 0; }
        pages += b;
        if (count > k) return false;
    }
    return true;
}
// Time: O(n log(sum))  Space: O(1)
```

---

### P7-54. Find the Element Appearing Once in Sorted Array
**Pattern:** Binary Search | **Key Idea:** All pairs at even index with next. If pair at mid is intact → single is to the right. Else to the left.

```java
public int singleNonDuplicate(int[] nums) {
    int lo = 0, hi = nums.length - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (mid % 2 == 1) mid--; // ensure mid is even
        if (nums[mid] == nums[mid + 1]) lo = mid + 2; // pair intact → go right
        else                            hi = mid;      // pair broken → go left
    }
    return nums[lo];
}
// Time: O(log n)  Space: O(1)
```

---

---

## Pattern 8 — Stack (2 problems)

> **When to use:** Monotone stack for histogram, next greater element, rectangle area.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 55 | Max Rectangle in Binary Matrix | 🔴 Hard | O(m×n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/max-rectangle/1) |
| 56 | Count Smaller Elements on Right | 🔴 Hard | O(n log n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/count-smaller-elements2214/1) |

---

### P8-55. Max Rectangle in Binary Matrix
**Pattern:** Stack (Histogram per row) | **Key Idea:** Treat each row as histogram heights. Apply largest-rectangle-in-histogram using stack for each row.

```java
public int maxRectangle(char[][] matrix) {
    int n = matrix[0].length, maxArea = 0;
    int[] heights = new int[n];
    for (char[] row : matrix) {
        for (int i = 0; i < n; i++)
            heights[i] = (row[i] == '1') ? heights[i] + 1 : 0;
        maxArea = Math.max(maxArea, largestRect(heights));
    }
    return maxArea;
}
private int largestRect(int[] h) {
    Stack<Integer> st = new Stack<>();
    int max = 0;
    for (int i = 0; i <= h.length; i++) {
        int curr = (i == h.length) ? 0 : h[i];
        while (!st.isEmpty() && curr < h[st.peek()]) {
            int ht = h[st.pop()];
            int w  = st.isEmpty() ? i : i - st.peek() - 1;
            max = Math.max(max, ht * w);
        }
        st.push(i);
    }
    return max;
}
// Time: O(m×n)  Space: O(n)
```

---

### P8-56. Count Smaller Elements on Right Side
**Pattern:** Merge Sort (Count Inversions) | **Key Idea:** When right element is placed before left during merge → right count of left element increases.

```java
int[] count;
public List<Integer> countSmaller(int[] nums) {
    int n = nums.length;
    count = new int[n];
    int[][] indexed = new int[n][2];
    for (int i = 0; i < n; i++) indexed[i] = new int[]{nums[i], i};
    mergeSort(indexed, 0, n - 1);
    List<Integer> result = new ArrayList<>();
    for (int c : count) result.add(c);
    return result;
}
private void mergeSort(int[][] arr, int l, int r) {
    if (l >= r) return;
    int m = (l + r) / 2;
    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);
    List<int[]> tmp = new ArrayList<>();
    int i = l, j = m + 1, rightCount = 0;
    while (i <= m && j <= r) {
        if (arr[j][0] < arr[i][0]) { tmp.add(arr[j++]); rightCount++; }
        else { count[arr[i][1]] += rightCount; tmp.add(arr[i++]); }
    }
    while (i <= m) { count[arr[i][1]] += rightCount; tmp.add(arr[i++]); }
    while (j <= r)  tmp.add(arr[j++]);
    for (int k = 0; k < tmp.size(); k++) arr[l + k] = tmp.get(k);
}
// Time: O(n log n)  Space: O(n)
```

---

---

## Pattern 9 — Dynamic Programming (16 problems)

> **When to use:** Optimal (max/min/count) + overlapping subproblems.  
> **Framework:** Define state → Write recurrence → Base case → Fill table bottom-up.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 57 | Longest Increasing Subsequence (LIS) | 🟡 Medium | O(n²) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/longest-increasing-subsequence-1587115620/1) |
| 58 | Longest Common Subsequence (LCS) | 🔴 Hard | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/longest-common-subsequence-1587115620/1) |
| 59 | Edit Distance | 🔴 Hard | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/edit-distance3702/1) |
| 60 | Partition Equal Subset Sum | 🔴 Hard | O(n·sum) | O(sum) | [Practice](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1) |
| 61 | Wildcard Pattern Matching | 🔴 Hard | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/wildcard-pattern-matching/1) |
| 62 | Form a Palindrome (Min Insertions) | 🔴 Hard | O(n²) | O(n²) | [Practice](https://www.geeksforgeeks.org/problems/form-a-palindrome1455/1) |
| 63 | Matrix Chain Multiplication | 🔴 Hard | O(n³) | O(n²) | [Practice](https://www.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1) |
| 64 | Minimum Number of Deletions (Palindrome) | 🔴 Hard | O(n²) | O(n²) | [Practice](https://www.geeksforgeeks.org/problems/minimum-number-of-deletions4610/1) |
| 65 | Probability of Knight | 🔴 Hard | O(k·n²) | O(n²) | [Practice](https://www.geeksforgeeks.org/problems/probability-of-knight5529/1) |
| 66 | Longest Common Substring | 🔴 Hard | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/longest-common-substring1452/1) |
| 67 | 0-1 Knapsack Problem | 🔴 Hard | O(n·W) | O(n·W) | [Practice](https://www.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1) |
| 68 | Longest Palindromic Substring | 🟡 Medium | O(n²) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/longest-palindrome-in-a-string1956/1) |
| 69 | Minimum Cost Path | 🟡 Medium | O(m×n) | O(m×n) | [Practice](https://www.geeksforgeeks.org/problems/minimum-cost-path3833/1) |
| 70 | House Robber | 🟡 Medium | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/max-sum-without-adjacents2430/1) |
| 71 | Max Length Chain of Pairs | 🟡 Medium | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/max-length-chain/1) |
| 72 | Smallest Positive Integer Not Representable as Subset Sum | 🟡 Medium | O(n log n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/smallest-positive-integer-that-can-not-be-represented-as-sum--141631/1) |

---

### P9-57. Longest Increasing Subsequence (LIS)
**Pattern:** DP | **Key Idea:** `dp[i]` = LIS length ending at index i. For each i, check all j < i where `nums[j] < nums[i]`.

```java
public int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);
    int maxLIS = 1;
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++)
            if (nums[j] < nums[i]) dp[i] = Math.max(dp[i], dp[j] + 1);
        maxLIS = Math.max(maxLIS, dp[i]);
    }
    return maxLIS;
}
// Time: O(n²)  Space: O(n)
// O(n log n) possible using patience sort (TreeSet / binary search on tails[])
```

---

### P9-58. Longest Common Subsequence (LCS)
**Pattern:** DP 2D | **Key Idea:** If chars match → `dp[i-1][j-1] + 1`. Else → `max(dp[i-1][j], dp[i][j-1])`.

```java
public int lcs(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = (s1.charAt(i-1) == s2.charAt(j-1))
                       ? dp[i-1][j-1] + 1
                       : Math.max(dp[i-1][j], dp[i][j-1]);
    return dp[m][n];
}
// Time: O(m×n)  Space: O(m×n)
```

---

### P9-59. Edit Distance
**Pattern:** DP 2D | **Key Idea:** `dp[i][j]` = min ops to convert `w1[0..i]` to `w2[0..j]`. Three choices: insert, delete, replace.

```java
public int editDistance(String w1, String w2) {
    int m = w1.length(), n = w2.length();
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = (w1.charAt(i-1) == w2.charAt(j-1))
                       ? dp[i-1][j-1]
                       : 1 + Math.min(dp[i-1][j-1], Math.min(dp[i-1][j], dp[i][j-1]));
    return dp[m][n];
}
// Time: O(m×n)  Space: O(m×n)
```

---

### P9-60. Partition Equal Subset Sum
**Pattern:** DP — 0/1 Knapsack | **Key Idea:** Total must be even. Find subset with sum = total/2. Traverse DP array right to left.

```java
public boolean canPartition(int[] nums) {
    int total = Arrays.stream(nums).sum();
    if (total % 2 != 0) return false;
    int target = total / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;
    for (int num : nums)
        for (int j = target; j >= num; j--) // RIGHT TO LEFT — key!
            dp[j] = dp[j] || dp[j - num];
    return dp[target];
}
// Time: O(n·sum)  Space: O(sum)
```

---

### P9-61. Wildcard Pattern Matching
**Pattern:** DP 2D | **Key Idea:** `*` → `dp[i-1][j]` (match empty) OR `dp[i][j-1]` (match one more). `?` or exact → `dp[i-1][j-1]`.

```java
public boolean isMatch(String text, String pattern) {
    int m = text.length(), n = pattern.length();
    boolean[][] dp = new boolean[m + 1][n + 1];
    dp[0][0] = true;
    for (int j = 1; j <= n; j++)
        if (pattern.charAt(j - 1) == '*') dp[0][j] = dp[0][j - 1];
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            char p = pattern.charAt(j - 1);
            if (p == '*')                       dp[i][j] = dp[i-1][j] || dp[i][j-1];
            else if (p == '?' || p == text.charAt(i-1)) dp[i][j] = dp[i-1][j-1];
        }
    }
    return dp[m][n];
}
// Time: O(m×n)  Space: O(m×n)
```

---

### P9-62. Form a Palindrome (Min Insertions)
**Pattern:** DP — LPS | **Key Idea:** Min insertions = n - LPS(s). LPS = LCS(s, reverse(s)).

```java
public int minInsertions(String s) {
    String rev = new StringBuilder(s).reverse().toString();
    return s.length() - lcs(s, rev); // reuse lcs() above
}
// Time: O(n²)  Space: O(n²)
```

---

### P9-63. Matrix Chain Multiplication
**Pattern:** DP — Interval | **Key Idea:** `dp[i][j]` = min multiplications for matrices i to j. Try every split point k.

```java
public int matrixChain(int[] dims) {
    int n = dims.length - 1; // number of matrices
    int[][] dp = new int[n][n];
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            dp[i][j] = Integer.MAX_VALUE;
            for (int k = i; k < j; k++) {
                int cost = dp[i][k] + dp[k+1][j] + dims[i] * dims[k+1] * dims[j+1];
                dp[i][j] = Math.min(dp[i][j], cost);
            }
        }
    }
    return dp[0][n - 1];
}
// Time: O(n³)  Space: O(n²)
```

---

### P9-64. Minimum Number of Deletions to Make Palindrome
**Pattern:** DP — LPS | **Key Idea:** Min deletions = n - LPS(s). Same approach as Form a Palindrome.

```java
public int minDeletions(String s) {
    String rev = new StringBuilder(s).reverse().toString();
    return s.length() - lcs(s, rev); // reuse lcs()
}
// Time: O(n²)  Space: O(n²)
```

---

### P9-65. Probability of Knight Remaining on Chessboard
**Pattern:** DP / BFS | **Key Idea:** `dp[r][c]` = probability of being at (r,c). Each step distribute prob / 8 to 8 valid neighbor moves.

```java
public double knightProbability(int n, int k, int r, int c) {
    int[][] moves = {{-2,-1},{-2,1},{-1,-2},{-1,2},{1,-2},{1,2},{2,-1},{2,1}};
    double[][] dp = new double[n][n];
    dp[r][c] = 1.0;
    for (int step = 0; step < k; step++) {
        double[][] next = new double[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++) {
                if (dp[i][j] == 0) continue;
                for (int[] m : moves) {
                    int ni = i + m[0], nj = j + m[1];
                    if (ni >= 0 && ni < n && nj >= 0 && nj < n)
                        next[ni][nj] += dp[i][j] / 8.0;
                }
            }
        dp = next;
    }
    double prob = 0;
    for (double[] row : dp) for (double v : row) prob += v;
    return prob;
}
// Time: O(k·n²)  Space: O(n²)
```

---

### P9-66. Longest Common Substring
**Pattern:** DP 2D | **Key Idea:** `dp[i][j]` = common substring length ending at s1[i] and s2[j]. Reset to 0 on mismatch.

```java
public int longestCommonSubstring(String s1, String s2) {
    int m = s1.length(), n = s2.length(), maxLen = 0;
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++) {
            if (s1.charAt(i-1) == s2.charAt(j-1)) {
                dp[i][j] = dp[i-1][j-1] + 1;
                maxLen = Math.max(maxLen, dp[i][j]);
            }
            // else dp[i][j] stays 0 — substring must be contiguous
        }
    return maxLen;
}
// Time: O(m×n)  Space: O(m×n)
```

---

### P9-67. 0-1 Knapsack Problem
**Pattern:** DP 2D | **Key Idea:** `dp[i][w]` = max value using first i items with capacity w. Either include item i or skip it.

```java
public int knapsack(int[] wt, int[] val, int W) {
    int n = wt.length;
    int[][] dp = new int[n + 1][W + 1];
    for (int i = 1; i <= n; i++)
        for (int w = 0; w <= W; w++) {
            dp[i][w] = dp[i-1][w]; // skip item i
            if (wt[i-1] <= w)      // include item i if it fits
                dp[i][w] = Math.max(dp[i][w], dp[i-1][w - wt[i-1]] + val[i-1]);
        }
    return dp[n][W];
}
// Time: O(n·W)  Space: O(n·W)
```

---

### P9-68. Longest Palindromic Substring
**Pattern:** Expand Around Center | **Key Idea:** For each center (odd + even length), expand while chars match. Track max.

```java
public String longestPalindrome(String s) {
    int start = 0, maxLen = 1;
    for (int i = 0; i < s.length(); i++) {
        for (int[] center : new int[][]{{i, i}, {i, i + 1}}) {
            int l = center[0], r = center[1];
            while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
                l--; r++;
            }
            if (r - l - 1 > maxLen) { maxLen = r - l - 1; start = l + 1; }
        }
    }
    return s.substring(start, start + maxLen);
}
// Time: O(n²)  Space: O(1)
```

---

### P9-69. Minimum Cost Path
**Pattern:** DP Grid | **Key Idea:** `dp[i][j]` = min cost to reach (i,j). Can come from top, left, or top-left diagonal.

```java
public int minCostPath(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            dp[i][j] = grid[i][j] + Math.min(dp[i-1][j],
                                     Math.min(dp[i][j-1], dp[i-1][j-1]));
    return dp[m-1][n-1];
}
// Time: O(m×n)  Space: O(m×n)
```

---

### P9-70. House Robber
**Pattern:** DP 1D | **Key Idea:** `dp[i]` = max money from first i houses. `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`. Optimize to 2 variables.

```java
public int rob(int[] nums) {
    int prev2 = 0, prev1 = 0;
    for (int num : nums) {
        int curr = Math.max(prev1, prev2 + num);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
// Time: O(n)  Space: O(1)
```

---

### P9-71. Max Length Chain of Pairs
**Pattern:** Greedy (Sort by End) | **Key Idea:** Sort by second element. Greedily pick a pair if its start > end of last picked pair.

```java
public int maxChainLength(int[][] pairs) {
    Arrays.sort(pairs, (a, b) -> a[1] - b[1]);
    int count = 1, end = pairs[0][1];
    for (int i = 1; i < pairs.length; i++)
        if (pairs[i][0] > end) { count++; end = pairs[i][1]; }
    return count;
}
// Time: O(n log n)  Space: O(1)
```

---

### P9-72. Smallest Positive Integer Not Representable as Subset Sum
**Pattern:** Greedy | **Key Idea:** Sort. Track `reach` (max sum representable so far). If `arr[i] > reach + 1` → answer is `reach + 1`.

```java
public int smallestNonRepresentable(int[] arr) {
    Arrays.sort(arr);
    int reach = 0;
    for (int num : arr) {
        if (num > reach + 1) break; // gap found
        reach += num;
    }
    return reach + 1;
}
// Time: O(n log n)  Space: O(1)
```

---

---

## Pattern 10 — Backtracking (1 problem)

> **When to use:** Enumerate all possibilities. Undo choice (backtrack) on dead end.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 73 | Generate Parentheses | 🟡 Medium | O(4ⁿ/√n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/generate-all-possible-parentheses/1) |

---

### P10-73. Generate Parentheses
**Pattern:** Backtracking | **Key Idea:** Add `(` if open < n. Add `)` if close < open. Stop when length = 2n.

```java
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<>();
    backtrack(result, new StringBuilder(), 0, 0, n);
    return result;
}
private void backtrack(List<String> res, StringBuilder cur,
                        int open, int close, int n) {
    if (cur.length() == 2 * n) { res.add(cur.toString()); return; }
    if (open < n) {
        cur.append('(');
        backtrack(res, cur, open + 1, close, n);
        cur.deleteCharAt(cur.length() - 1);
    }
    if (close < open) {
        cur.append(')');
        backtrack(res, cur, open, close + 1, n);
        cur.deleteCharAt(cur.length() - 1);
    }
}
// Time: O(4ⁿ/√n)  Space: O(n) stack depth
```

---

---

## Pattern 11 — Linked List (1 problem)

> **When to use:** Slow/Fast pointer = O(1) space for cycle detection, middle finding.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 74 | Detect Cycle in a Linked List | 🔴 Hard | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/detect-loop-in-linked-list/1) |

---

### P11-74. Detect Cycle in a Linked List
**Pattern:** Floyd's Cycle Detection | **Key Idea:** Slow moves 1 step, fast moves 2. If they ever meet → cycle exists.

```java
// class ListNode { int val; ListNode next; }
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true; // cycle detected
    }
    return false; // fast reached null → no cycle
}
// Time: O(n)  Space: O(1)
```

---

---

## Pattern 12 — String Manipulation (5 problems)

> **When to use:** Char frequency array (size 26), StringBuilder, or Two Pointers on string.

| # | Problem | Difficulty | Time | Space | Practice |
|---|---------|------------|------|-------|----------|
| 75 | Check if Array is Sorted | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/check-if-an-array-is-sorted0701/1) |
| 76 | Remove Common Characters and Concatenate | 🟢 Easy | O(m+n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/remove-common-characters-and-concatenate-1587115621/1) |
| 77 | Check if String is Rotated by Two Places | 🟢 Easy | O(n) | O(n) | [Practice](https://www.geeksforgeeks.org/problems/check-if-string-is-rotated-by-two-places-1587115620/1) |
| 78 | Sort String of Characters | 🟢 Easy | O(n) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/sort-a-string2943/1) |
| 79 | Sum Palindrome | 🟢 Easy | O(d) | O(1) | [Practice](https://www.geeksforgeeks.org/problems/sum-palindrome3857/1) |

---

### P12-75. Check if Array is Sorted
**Pattern:** Linear Scan | **Key Idea:** Single pass. If any element < previous → not sorted.

```java
public boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++)
        if (arr[i] < arr[i - 1]) return false;
    return true;
}
// Time: O(n)  Space: O(1)
```

---

### P12-76. Remove Common Characters and Concatenate
**Pattern:** Set / Frequency Array | **Key Idea:** Find chars common to both. Append uncommon chars from each string.

```java
public String removeCommon(String s1, String s2) {
    Set<Character> common = new HashSet<>();
    for (char c : s1.toCharArray())
        if (s2.indexOf(c) >= 0) common.add(c);
    StringBuilder sb = new StringBuilder();
    for (char c : s1.toCharArray()) if (!common.contains(c)) sb.append(c);
    for (char c : s2.toCharArray()) if (!common.contains(c)) sb.append(c);
    return sb.toString();
}
// Time: O(m+n)  Space: O(1)
```

---

### P12-77. Check if String is Rotated by Two Places
**Pattern:** String | **Key Idea:** Two cases — left rotate by 2, right rotate by 2. Compare both with s2.

```java
public boolean isRotatedBy2(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    int n = s1.length();
    String leftRot  = s1.substring(2) + s1.substring(0, 2);
    String rightRot = s1.substring(n - 2) + s1.substring(0, n - 2);
    return s2.equals(leftRot) || s2.equals(rightRot);
}
// Time: O(n)  Space: O(n)
```

---

### P12-78. Sort String of Characters
**Pattern:** Counting Sort | **Key Idea:** Count frequency of each character. Rebuild in sorted order.

```java
public String sortString(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 26; i++)
        for (int j = 0; j < freq[i]; j++) sb.append((char)('a' + i));
    return sb.toString();
}
// Time: O(n)  Space: O(1)
```

---

### P12-79. Sum Palindrome
**Pattern:** Math | **Key Idea:** n + reverse(n) should itself be a palindrome. Verify by reversing the sum.

```java
public boolean isSumPalindrome(int n) {
    int rev = reverse(n);
    int sum = n + rev;
    return sum == reverse(sum);
}
private int reverse(int n) {
    int rev = 0;
    while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
    return rev;
}
// Time: O(d)  Space: O(1)
```

---

---

## Quick Revision Cheatsheet

| Pattern | Trigger Words | Key Technique |
|---------|--------------|---------------|
| Math / Logic | formula, digits, prime, GCD | Direct formula / loop |
| Two Pointers | sorted + pair/triplet, palindrome, in-place | L=0, R=n-1, move based on condition |
| Bit Manipulation | lone element, XOR, binary | `a^a=0`, `a^0=a` |
| Greedy | min platforms, job schedule, jump | Sort first, pick locally optimal |
| Sliding Window | subarray with sum/condition | Expand right, shrink left |
| Prefix Sum | count subarrays with sum=k | HashMap of prefix sums |
| Kadane's | max subarray | `curr = max(num, curr+num)` |
| HashMap | frequency, two sum, duplicates | O(1) lookup |
| Binary Search | sorted / monotone answer space | `lo + (hi-lo)/2`, shrink window |
| Stack | histogram, rectangle, monotone | Pop when condition breaks |
| DP | optimal + overlapping subproblems | State → Recurrence → Table |
| Backtracking | all combinations, permutations | Try → Recurse → Undo |
| Slow/Fast Ptr | cycle detection, middle of LL | Fast moves 2x speed |

---

*Total: 79 problems | 12 patterns | Java solutions with Time & Space complexity*
