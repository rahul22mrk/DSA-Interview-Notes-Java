# Infosys SDE Sheet — Revision Sheet
> **79 Problems | Pattern-wise | Approach included**
> 🟢 Easy: 39 | 🟡 Medium: 22 | 🔴 Hard: 14

---

## Pattern 1 — Math / Logic / Basics (29 problems)
> **When to use:** No DS needed. Formula, loop, ya simple conditionals.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 1 | Count Digits | 🟢 | `n /= 10` karte jao jab tak n > 0, har baar count++. Ya ek liner: `(int)log10(n) + 1` | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/count-digits-1606889545/1) |
| 2 | Print First N Fibonacci | 🟢 | a=0, b=1 rakho. Loop mein c=a+b, print c, phir a=b aur b=c. Recursion mat use karo — O(2^n) ho jaata | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/print-first-n-fibonacci-numbers1002/1) |
| 3 | Armstrong Number | 🟢 | Pehle total digits count karo. Phir har digit ko `digit^totalDigits` pe raise karo aur sum karo. Sum == original → Armstrong | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/armstrong-numbers2727/1) |
| 4 | Area of Rect, Triangle, Circle | 🟢 | Rect = l×w. Triangle = 0.5×b×h. Circle = π×r². Seedha formula. `9.0/5.0` use karo integer division avoid karne ke liye | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/area-of-rectange-right-angled-triangle-and-circle2600/1) |
| 5 | Two Matrices Identical | 🟢 | Pehle dimensions check karo. Phir double loop mein har `A[i][j] != B[i][j]` pe false. Poora match hoga to true | O(m×n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/identical-matrices1042/1) |
| 6 | Add Two Matrices | 🟢 | Result matrix banao. Double loop: `C[i][j] = A[i][j] + B[i][j]`. Bas | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/addition-of-two-square-matrices4916/1) |
| 7 | Any Base to Decimal | 🟢 | Right se left iterate karo. Har digit ko `digit × base^position` se multiply karo, sum karo. Letter digits ke liye: `c - 'A' + 10` | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/convert-from-any-base-to-decimal3736/1) |
| 8 | Celsius to Fahrenheit | 🟢 | Formula: `F = (C × 9.0 / 5.0) + 32`. 9.0 isliye ki integer division na ho | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/celsius-to-fahrenheit-conversion5212/1) |
| 9 | Print 1 to N (No Loop) | 🟢 | `f(n-1)` pehle call karo, phir `print(n)`. Aise recursion stack pe ascending order milta hai. Agar pehle print karo to descending aata | O(n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/print-1-to-n-without-using-loops3621/1) |
| 10 | Middle of Three | 🟢 | Trick: `a + b + c - max(a,b,c) - min(a,b,c)` = middle. Teen mein se sabse bada aur sabse chhota hatao, bacha middle | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/middle-of-three2926/1) |
| 11 | Greatest of Three | 🟢 | `Math.max(a, Math.max(b, c))`. Ya simple if-else chain | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/greatest-of-three-numbers2520/1) |
| 12 | Number of Open Doors | 🟢 | Door i toggle hoti hai by every divisor of i. Odd divisors wali doors khuli rahegi. Sirf perfect squares ki odd number of divisors hoti hain. Answer = `floor(√n)` | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/number-of-open-doors1552/1) |
| 13 | Max Sum of Products | 🟢 | Dono arrays sort karo. i-th largest × i-th largest pair karo. Rearrangement inequality: largest × largest = max sum | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/maximum-possible-sum-of-products3637/1) |
| 14 | Four Points = Square? | 🟢 | 4 points ke 6 pairwise distances² nikalo. Sort karo. Agar `d[0]==d[1]==d[2]==d[3]` (4 equal sides) AND `d[4]==d[5]` (2 equal diagonals) AND `d[0] > 0` → square | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/check-if-given-four-points-form-a-square3026/1) |
| 15 | Overlapping Rectangles | 🟢 | Overlap nahi hoga agar: ek rect dusre ke completely left mein (`x1>=x4` ya `x3>=x2`), ya completely upar/neeche (`y1>=y4` ya `y3>=y2`). Inme se koi bhi true → no overlap | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/overlapping-rectangles1924/1) |
| 16 | Sum of Primes 1 to N | 🟢 | Sieve of Eratosthenes: boolean `isComposite[]` array. i=2 se start: prime mila to uske saare multiples mark karo. Jo marked nahi woh prime hain — unka sum | O(n log log n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/sum-of-all-prime-numbers-between-1-and-n4404/1) |
| 17 | Power of Another Number | 🟢 | `curr = base`. Jab tak `curr < n` → `curr *= base`. Agar `curr == n` → yes. Edge: base=1 → sirf n=1 pe true | O(log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/check-if-a-number-is-power-of-another-number5442/1) |
| 18 | Common Divisors | 🟢 | Pehle `GCD(a,b)` nikalo. Common divisors of a and b = all divisors of GCD. `√g` loop se sare divisors nikalo (i aur g/i dono add karo) | O(√g) | O(d) | [🔗](https://www.geeksforgeeks.org/problems/common-divisors4712/1) |
| 19 | Perfect Number | 🟢 | sum=1 se start (1 hamesha proper divisor). i=2 to √n: `n%i==0` → `sum += i + n/i`. Agar `i == n/i` to sirf ek baar add karo. sum==n → perfect | O(√n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/perfect-number3759/1) |
| 20 | Sum Palindrome | 🟢 | `sum = n + reverse(n)`. Phir check karo `sum == reverse(sum)`. Haan → Sum Palindrome. Reverse: `rev = rev*10 + n%10, n/=10` loop | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/sum-palindrome3857/1) |
| 21 | Check Valid Date | 🟢 | Step 1: month 1-12. Step 2: `daysInMonth[]` array banao {31,28,31...}. Step 3: leap year check karo `(y%4==0 && y%100!=0) \|\| y%400==0` → Feb=29. Step 4: day ≤ daysInMonth[m-1] | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/check-date-valid-or-not/1) |
| 22 | Lazy Caterer's Problem | 🟢 | Formula: n cuts se max pieces = `n(n+1)/2 + 1`. Har nayi cut maximum n existing lines cross karti hai, utne naye pieces banate | O(1) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/the-lazy-caterers-problem2527/1) |
| 23 | Print Sum Triangle | 🟢 | Original array = bottom row. Naya row = adjacent elements ka sum (size ek kam). Upar build karte jao. Print top to bottom | O(n²) | O(n²) | [🔗](https://www.geeksforgeeks.org/problems/sum-triangle-for-given-array1159/1) |
| 24 | Largest Number from Digits | 🟢 | Digits ko descending sort karo. Concatenate karo. E.g. [9,1,3] → "931" | O(n log n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/form-largest-number-from-digits5430/1) |
| 25 | Print the Left Element | 🟢 | Sort karo. lo=0, hi=n-1. Alternate: min remove (lo++), max remove (hi--). Jab lo==hi → `arr[lo]` answer | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/print-the-left-element2009/1) |
| 26 | Tidy Number | 🟢 | String mein convert karo. Left to right: agar `s[i] < s[i-1]` → not tidy. Poori string pass ho → tidy | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/tidy-number0519/1) |
| 27 | Mean of Array | 🟢 | `long sum = 0`. Sab elements add karo. `(double)sum / n`. Long use karo overflow se bachne ke liye | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/mean0021/1) |
| 28 | String Rotated by 2 Places | 🟢 | Do cases check karo: Left rotate 2 = `s[2..] + s[0..1]`. Right rotate 2 = `s[n-2..] + s[0..n-3]`. Dono mein se koi s2 se match kare → true | O(n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/check-if-string-is-rotated-by-two-places-1587115620/1) |
| 29 | Binary Representation | 🟢 | `n & 1` se LSB nikalo, prepend karo result mein. `n >>= 1` right shift. Jab tak n > 0. Alt: `Integer.toBinaryString(n)` | O(log n) | O(log n) | [🔗](https://www.geeksforgeeks.org/problems/binary-representation5003/1) |

---

## Pattern 2 — Two Pointers (6 problems)
> **When to use:** Sorted array mein pair/triplet dhundhna, in-place modify, palindrome.
> **Rule:** `sum < target → L++` | `sum > target → R--` | Sort first!

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 30 | Pair with Given Sum | 🟢 | Sort karo. L=0, R=n-1. `sum = arr[L]+arr[R]`. Target se chhota → L++, bada → R--, equal → pair mila. Loop jab tak L < R | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/count-pairs-with-given-sum5022/1) |
| 31 | Remove Duplicates (Sorted Array) | 🟢 | slow=0 (write ptr), fast=1 se loop. Agar `arr[fast] != arr[slow]` → `arr[++slow] = arr[fast]`. Return `slow+1`. Fast hamesha padhta, slow sirf naye element pe likhta | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/remove-duplicate-elements-from-sorted-array/1) |
| 32 | Merge Two Sorted (No Extra Space) | 🟡 | End se start karo. i=m-1, j=n-1, k=m+n-1. Dono mein jo bada ho → `arr1[k--]` pe rakho, us pointer ko decrement karo. j remaining ho to copy karo | O(m+n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1) |
| 33 | Sentence Palindrome | 🟢 | L=0, R=end. Non-alphanumeric skip karo. `toLowerCase` compare karo. Match nahi → false. Match → L++, R--. Loop jab tak L < R | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/string-palindromic-ignoring-spaces4723/1) |
| 34 | Reverse a String | 🟢 | char[] banao. L=0, R=n-1. Swap `arr[L]` and `arr[R]`. L++, R--. Jab tak L < R | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/reverse-a-string/1) |
| 35 | Next Permutation | 🟡 | **Step 1:** Right se `nums[i] < nums[i+1]` dhundho (pivot i). **Step 2:** i ke right mein `nums[j] > nums[i]` wala rightmost j. **Step 3:** i aur j swap karo. **Step 4:** i+1 to end reverse karo. Pivot na mile → poora reverse | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/next-permutation5226/1) |

---

## Pattern 3 — Bit Manipulation (2 problems)
> **Rules:** `a ^ a = 0` | `a ^ 0 = a` | XOR commutative & associative

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 36 | Party of Couples (Lone Person) | 🟢 | `result = 0`. Sab elements XOR karo `result ^= arr[i]`. Pairs cancel (a^a=0). Jo bache woh lone element. Ek line mein! | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/alone-in-couple5507/1) |
| 37 | Distinct Subset Sums | 🔴 | Sort karo. `dp = Set{0}`. Har element ke liye: `next = dp` copy karo, phir dp ke har sum mein `num` add karo aur next mein daalo. `dp = next`. End mein sorted list return | O(n·2ⁿ) | O(2ⁿ) | [🔗](https://www.geeksforgeeks.org/problems/find-all-distinct-subset-or-subsequence-sums4424/1) |

---

## Pattern 4 — Sorting / Greedy (7 problems)
> **When to use:** "Minimum possible", scheduling, arrangement problems.
> **Key:** Sort first, phir greedy choice lo.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 38 | Minimum Platforms | 🟡 | Arrivals aur Departures dono alag sort karo. i=1, j=0, platforms=1. Agar `arr[i] <= dep[j]` → nayi train aayi, platforms++, i++. Else → train gayi, platforms--, j++. Max track karo | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1) |
| 39 | Job Sequencing | 🟡 | Jobs ko profit desc sort karo. Har job ke liye deadline se 1 tak loop: pehla khali slot milo → assign karo aur break. Total count aur profit track karo | O(n log n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1) |
| 40 | Largest Number from Array | 🟡 | Custom comparator: `(a,b) → (b+a).compareTo(a+b)`. "3" vs "30": "330" > "303" → "3" pehle. All zeros edge case handle karo | O(n log n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/largest-number-formed-from-an-array1117/1) |
| 41 | Minimum Jumps | 🟡 | `farthest` = abhi tak max reachable. `currEnd` = current jump ki boundary. i loop: `farthest = max(farthest, i+nums[i])`. Jab `i == currEnd` → jump karo, jumps++, `currEnd = farthest` | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/minimum-number-of-jumps-1587115620/1) |
| 42 | Minimize Heights II | 🟡 | Sort karo. Base = `arr[n-1] - arr[0]`. Har i pe split: 0..i ko +k, i+1..n-1 ko -k. `maxH = max(arr[i]+k, arr[n-1]-k)`, `minH = min(arr[0]+k, arr[i+1]-k)`. minH<0 skip. result = min(maxH-minH) | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/minimize-the-heights3351/1) |
| 43 | Rotate Array | 🟡 | **3 reverse trick:** `k %= n`. Step 1: poora array reverse. Step 2: 0 to k-1 reverse. Step 3: k to n-1 reverse. In-place O(1) space | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/rotate-array-by-n-elements-1587115621/1) |
| 44 | Sort String of Characters | 🟢 | `freq[26]` array banao. Har char pe `freq[c-'a']++`. Phir i=0 to 25: `freq[i]` times `(char)('a'+i)` append karo. Counting sort — O(n) | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/sort-a-string2943/1) |

---

## Pattern 5 — Sliding Window / Prefix Sum / Kadane's (4 problems)
> **When to use:** Contiguous subarray mein optimize/count karna ho.
> **Rule:** Right expand hamesha. Left shrink tabhi jab condition violate ho.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 45 | Subarray with Given Sum | 🟡 | left=0, sum=0. Right expand: `sum += arr[right]`. Jab `sum > target`: `sum -= arr[left], left++`. Jab `sum == target` → mila. Non-negative numbers ke liye hi kaam karta | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1) |
| 46 | Subarrays with Sum = k | 🟡 | `map.put(0,1)` (empty prefix). Har index: `sum += num`. `count += map.get(sum-k)` — iska matlab: sum-k wala prefix pehle kahan tha, wahan se yahan tak sum = k. Phir `map.put(sum, freq+1)` | O(n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1) |
| 47 | Kadane's — Max Subarray | 🟡 | `currSum = max(nums[i], currSum + nums[i])`. Agar current element akela zyada de raha → naya subarray shuru. `maxSum = max(maxSum, currSum)` har step pe update | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/kadanes-algorithm-1587115620/1) |
| 48 | Buy & Sell Stock | 🟢 | `minPrice = MAX_VALUE`. Har price: `minPrice = min(minPrice, price)`, phir `maxProfit = max(maxProfit, price - minPrice)`. Single pass. Pehle cheapest buy track, phir max profit | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/buy-stock-2/1) |

---

## Pattern 6 — HashMap / Frequency (3 problems)
> **When to use:** Counting, O(1) lookup, majority element.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 49 | Count Frequencies | 🟢 | Single pass: `freq.put(x, freq.getOrDefault(x,0) + 1)`. Phir map iterate karke print | O(n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/frequency-of-elements--111353/1) |
| 50 | Majority Element (> n/2) | 🟡 | Boyer-Moore Voting: `candidate = nums[0], count = 1`. Loop: `count==0` → naya candidate. `nums[i]==candidate` → count++. Else count--. End mein candidate return | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/majority-element-1587115620/1) |
| 51 | Remove Common Chars & Concat | 🟢 | Common chars Set mein daalo (s1 ke jo s2 mein bhi hain). s1 se common wale hata ke append, phir s2 se hata ke append | O(m+n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/remove-common-characters-and-concatenate-1587115621/1) |

---

## Pattern 7 — Binary Search (3 problems)
> **When to use:** Sorted input ya monotone answer space (feasibility check ho sake).
> **Template:** `mid = lo + (hi - lo) / 2` — overflow se bachne ke liye hamesha yahi.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 52 | Binary Search | 🟢 | lo=0, hi=n-1. `mid = lo+(hi-lo)/2`. `arr[mid]==target` → return. `arr[mid] < target` → `lo=mid+1`. Else `hi=mid-1`. Loop jab tak lo <= hi | O(log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/binary-search-1587115620/1) |
| 53 | Allocate Min Pages | 🟡 | Answer space: `lo=max(arr)`, `hi=sum(arr)`. Har mid ke liye feasibility check: m students mein distribute ho sakta hai agar max pages = mid? Feasible → `hi=mid-1`, ans=mid. Else `lo=mid+1` | O(n log S) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) |
| 54 | Element Once in Sorted Array | 🟡 | Sab elements pairs mein. Even index pe pair hona chahiye. mid ko even banao. Agar `arr[mid]==arr[mid+1]` → pair intact, single right mein → `lo=mid+2`. Else → single left mein → `hi=mid` | O(log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/element-appearing-once2552/1) |

---

## Pattern 8 — Stack (2 problems)
> **When to use:** Histogram area, next greater element, monotone structure.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 55 | Max Rectangle in Matrix | 🔴 | Har row ke baad ek histogram banta hai (consecutive 1s ki height). Us histogram pe **Largest Rectangle in Histogram** solve karo using monotone stack. Stack mein indices rakho. Jab `curr < h[stack.top]` → pop, `area = height × width` calculate karo (width = i - stack.top - 1) | O(m×n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/max-rectangle/1) |
| 56 | Count Smaller on Right | 🔴 | Modified merge sort use karo. Merge ke time: jab right element left se pehle place hota hai → `rightCount++`. Jab left element place hota hai → `count[original_index] += rightCount`. Index track karne ke liye `{value, originalIndex}` pairs rakho | O(n log n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/count-smaller-elements2214/1) |

---

## Pattern 9 — Dynamic Programming (16 problems)
> **When to use:** Max/Min/Count + choices at each step + overlapping subproblems.
> **Framework:** State define → Recurrence likho → Base case → Bottom-up fill.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 57 | LIS | 🟡 | `dp[i]` = LIS length ending at i (sab 1 se start). Har i ke liye sab j < i check: `nums[j] < nums[i]` → `dp[i] = max(dp[i], dp[j]+1)`. Answer = max(dp[]) | O(n²) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/longest-increasing-subsequence-1587115620/1) |
| 58 | LCS | 🔴 | `dp[i][j]` = LCS of s1[0..i-1] and s2[0..j-1]. Chars match → `dp[i-1][j-1] + 1`. No match → `max(dp[i-1][j], dp[i][j-1])` (skip ek char from either). Base: dp[0][x]=dp[x][0]=0 | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/longest-common-subsequence-1587115620/1) |
| 59 | Edit Distance | 🔴 | `dp[i][j]` = min ops to convert w1[0..i] to w2[0..j]. Match → `dp[i-1][j-1]`. No match → `1 + min(replace=dp[i-1][j-1], delete=dp[i-1][j], insert=dp[i][j-1])`. Base: dp[i][0]=i, dp[0][j]=j | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/edit-distance3702/1) |
| 60 | Partition Equal Subset | 🔴 | Total odd → false. target = sum/2. `dp[0]=true`. Har num ke liye **RIGHT TO LEFT** `j = target to num`: `dp[j] = dp[j] OR dp[j-num]`. Right to left isliye ki ek item ek hi baar use ho (0/1 property) | O(n·sum) | O(sum) | [🔗](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1) |
| 61 | Wildcard Matching | 🔴 | `dp[i][j]` = kya pattern[0..j-1] matches text[0..i-1]. `*` → `dp[i-1][j]` (match 1 char) OR `dp[i][j-1]` (match empty). `?` ya exact match → `dp[i-1][j-1]`. Base: `dp[0][j]=true` jab tak `*` hai | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/wildcard-pattern-matching/1) |
| 62 | Form a Palindrome (Min Insertions) | 🔴 | LPS (Longest Palindromic Subsequence) = `LCS(s, reverse(s))`. Min insertions = `n - LPS`. Jo chars already palindrome form karte hain unhe mat chhuo, baaki ke liye insert karo | O(n²) | O(n²) | [🔗](https://www.geeksforgeeks.org/problems/form-a-palindrome1455/1) |
| 63 | Matrix Chain Multiplication | 🔴 | `dp[i][j]` = min ops for matrices i to j. Length 2 se n tak loop. Har (i,j) ke liye k=i to j-1 split try: `cost = dp[i][k] + dp[k+1][j] + dims[i]*dims[k+1]*dims[j+1]`. Min lo | O(n³) | O(n²) | [🔗](https://www.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1) |
| 64 | Min Deletions for Palindrome | 🔴 | Same as Form a Palindrome. `min deletions = n - LPS(s)`. LPS = LCS(s, reverse(s)). Jo LPS mein nahi → delete karna padega | O(n²) | O(n²) | [🔗](https://www.geeksforgeeks.org/problems/minimum-number-of-deletions4610/1) |
| 65 | Probability of Knight | 🔴 | `dp[r][c]` = prob of being at (r,c). Start pe `dp[sr][sc]=1.0`. Har step: `next[ni][nj] += dp[i][j] / 8.0` for all 8 valid knight moves. k steps ke baad sab dp values ka sum = final probability | O(k·n²) | O(n²) | [🔗](https://www.geeksforgeeks.org/problems/probability-of-knight5529/1) |
| 66 | Longest Common Substring | 🔴 | LCS se farq: substring contiguous honi chahiye. `dp[i][j]` = common substring ending at s1[i] and s2[j]. Match → `dp[i-1][j-1]+1`. **No match → 0** (restart! LCS mein max(skip) hota tha, yahan nahi). maxLen track karo | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/longest-common-substring1452/1) |
| 67 | 0-1 Knapsack | 🔴 | `dp[i][w]` = max value using first i items with capacity w. Do choices: Skip → `dp[i-1][w]`. Include (agar `wt[i-1] <= w`) → `dp[i-1][w-wt[i-1]] + val[i-1]`. Dono ka max lo | O(n·W) | O(n·W) | [🔗](https://www.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1) |
| 68 | Longest Palindromic Substring | 🟡 | Har index pe do centers: odd `(i,i)` aur even `(i,i+1)`. Dono taraf expand karo jab tak chars match hon. `r-l-1` = length. Sab centers mein max track karo | O(n²) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/longest-palindrome-in-a-string1956/1) |
| 69 | Minimum Cost Path | 🟡 | `dp[i][j] = grid[i][j] + min(dp[i-1][j] upar, dp[i][j-1] left, dp[i-1][j-1] diagonal)`. Teen directions. First row aur col alag fill karo (sirf ek direction se aa sakte) | O(m×n) | O(m×n) | [🔗](https://www.geeksforgeeks.org/problems/minimum-cost-path3833/1) |
| 70 | House Robber | 🟡 | `curr = max(prev1, prev2 + num)`. Ya toh is ghar skip karo (prev1), ya isko rob karo (prev2 + current). Do variables mein optimize: `prev2=prev1, prev1=curr` | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/max-sum-without-adjacents2430/1) |
| 71 | Max Length Chain | 🟡 | Pairs ko second element (end) se sort karo. `end=pairs[0][1]`, count=1. Agle pair: agar `pair[0] > end` → chain extend, count++, end update. Greedy: earliest ending wala lo — zyada options khule rahenge | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/max-length-chain/1) |
| 72 | Smallest Non-Representable Sum | 🟡 | Sort karo. `reach=0` (matlab 1 to reach represent kar sakte hain). Har element: agar `arr[i] > reach+1` → gap hai, `reach+1` nahi bana sakte → answer. Else `reach += arr[i]`. Loop ke baad → `reach+1` | O(n log n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/smallest-positive-integer-that-can-not-be-represented-as-sum--141631/1) |

---

## Pattern 10 — Backtracking (1 problem)
> **When to use:** Saari possibilities enumerate karni ho. Try → Recurse → Undo.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 73 | Generate Parentheses | 🟡 | `open` aur `close` count rakho. `open < n` → `(` add kar sakte. `close < open` → `)` add kar sakte (tabhi valid). Base: `length == 2n` → result mein add. Recursion ke baad last char delete karo (backtrack) | O(4ⁿ/√n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/generate-all-possible-parentheses/1) |

---

## Pattern 11 — Linked List (1 problem)
> **When to use:** Cycle detection, middle finding — O(1) space.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 74 | Detect Cycle in Linked List | 🔴 | slow aur fast dono head pe. Loop: `slow=slow.next`, `fast=fast.next.next`. Agar `slow==fast` → cycle. Fast ya fast.next null → no cycle. Fast 2x speed se move karta, cycle mein milna guaranteed | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/detect-loop-in-linked-list/1) |

---

## Pattern 12 — String Manipulation (5 problems)
> **When to use:** Character frequency, rotation, uncommon chars.

| # | Problem | Diff | Approach | Time | Space | Practice |
|---|---------|------|----------|------|-------|----------|
| 75 | Check if Array is Sorted | 🟢 | i=1 se loop. `arr[i] < arr[i-1]` → false. Poora loop bina false ke → true. Single pass | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/check-if-an-array-is-sorted0701/1) |
| 76 | Remove Common & Concatenate | 🟢 | Common chars Set mein daalo. s1 mein se common wale skip, baaki append. s2 mein se bhi same. Dono concatenate | O(m+n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/remove-common-characters-and-concatenate-1587115621/1) |
| 77 | String Rotated by 2 Places | 🟢 | Left rotate = `s[2..] + s[0..1]`. Right rotate = `s[n-2..] + s[0..n-3]`. Dono check karo s2 se. Koi match kare → true | O(n) | O(n) | [🔗](https://www.geeksforgeeks.org/problems/check-if-string-is-rotated-by-two-places-1587115620/1) |
| 78 | Sort String of Characters | 🟢 | `freq[26]` array. Har char `freq[c-'a']++`. i=0 to 25: `freq[i]` times `(char)('a'+i)` append karo | O(n) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/sort-a-string2943/1) |
| 79 | Sum Palindrome | 🟢 | `sum = n + reverse(n)`. Phir `sum == reverse(sum)` check karo. Haan → Sum Palindrome | O(d) | O(1) | [🔗](https://www.geeksforgeeks.org/problems/sum-palindrome3857/1) |

---

## ⚡ Pattern Recognition — Ek Nazar Mein

| Pattern | Trigger | Core Technique |
|---------|---------|----------------|
| Math/Logic | digits, prime, GCD, formula, geometry | Direct formula / loop |
| Two Pointers | sorted + pair, palindrome, in-place | L=0 R=n-1, condition pe move |
| Slow/Fast Pointer | cycle, middle of LL | fast 2×, slow 1× |
| Bit Manipulation | lone element, XOR, binary | `a^a=0`, `a^0=a` |
| Sliding Window | contiguous subarray sum/condition | expand right, shrink left |
| Prefix Sum + Map | count subarrays sum=k | `map.get(currSum - k)` |
| Kadane's | max subarray sum | `curr = max(num, curr+num)` |
| Greedy | scheduling, jump, min-max arrange | sort first, locally optimal |
| Custom Sort | largest number, pair arrangement | comparator override |
| HashMap | frequency, majority, duplicates | O(1) lookup |
| Binary Search | sorted / "min possible max" | `lo+(hi-lo)/2`, feasibility |
| Monotone Stack | histogram, rectangle, next greater | pop when condition breaks |
| DP 1D | house robber, LIS | dp[i] from dp[i-1], dp[i-2] |
| DP 2D | LCS, edit dist, knapsack | dp[i][j] from prev row/col |
| DP Interval | matrix chain | dp[i][j], try all k splits |
| Backtracking | generate all combos | try → recurse → undo |

---

## 🔴 Hard Problems — Ye Tricks Yaad Rakhna

| # | Problem | The One Trick |
|---|---------|---------------|
| 37 | Distinct Subset Sums | Sort + DP Set: `next = dp ∪ {s+num for s in dp}` |
| 55 | Max Rectangle | Row → histogram → monotone stack. width = `i - stack.peek() - 1` |
| 56 | Count Smaller on Right | Merge sort mein right place hone pe `rightCount++`, left place pe `count[idx] += rightCount` |
| 58 | LCS | Match=diagonal+1. No match=max(skip either char) |
| 59 | Edit Distance | No match = `1 + min(replace, delete, insert)` — teen options |
| 60 | Partition Equal Subset | **RIGHT TO LEFT** traverse — reuse avoid karne ke liye |
| 61 | Wildcard `*` | `dp[i-1][j]` (match 1) OR `dp[i][j-1]` (match 0) |
| 62 | Form a Palindrome | `n - LCS(s, reverse(s))` |
| 63 | Matrix Chain | Cost at split k = `dims[i] × dims[k+1] × dims[j+1]` |
| 64 | Min Deletions Palindrome | Same as Form a Palindrome: `n - LCS(s, reverse(s))` |
| 65 | Probability of Knight | Layer by layer: `next[ni][nj] += dp[i][j] / 8.0` |
| 66 | Common Substring | No match = **0** (not max like LCS — must be contiguous!) |
| 67 | 0-1 Knapsack | Include ya skip — `max(dp[i-1][w], dp[i-1][w-wt]+val)` |
| 74 | Detect Cycle | slow×1 + fast×2, milenge to cycle confirmed |

---
*79 problems · 12 patterns · Approach with every problem*
