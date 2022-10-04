# 數學主題總結

### 基礎數學

1. 中位數
    
    
    |  | 數學 | C++ | Java | Python |
    | --- | --- | --- | --- | --- |
    | 左中位數 | = (left + right) / 2 | = left + (right - left) / 2 | = left + (right - left) / 2 | = (left + right) // 2 |
    | 右中位數 | = (left + right + 1) / 2 | = left + (right - left + 1) / 2 | = left + (right - left + 1) / 2 | = (left + right + 1) // 2 |
    
    Leetcode練習：[**4. Median of Two Sorted Arrays**](https://leetcode.com/problems/median-of-two-sorted-arrays/)
    
2. x / m取整數
    
    int x, int y
    
    |  | 數學 | C++ | Java | Python |
    | --- | --- | --- | --- | --- |
    | 向下取整 | = ⌊x / y⌋ | = x / y
    = int(floor(1.0 * x / y)) | = x / y
    = (int) Math.floor(1.0 * x / y) | = x // y
    = int(math.floor(x / y)) |
    | 向上取整 | = ⌈x / y⌉ | = (x + y - 1) / y
    = int(ceil(1.0 * x / y)) | = (x + y - 1) / y
    = (int) Math.ceil(1.0 * x / y) | = (x + y - 1) // y
    = int(math.ceil(x / y)) |
    
    Leetcode練習：[**875. Koko Eating Bananas**](https://leetcode.com/problems/koko-eating-bananas/)
    
3. b進位制 與 數字反轉
    - 10進位數字反轉(Reverse Number)
        
        Time: O(log(num))
        
        Space: O(1)
        
        ```cpp
        int reverse(int num) {
        		int res = 0;
        		while (num > 0) {
        				res = 10 * res + num % 10; // 將末位數字append到res的後面
        				num /= 10; // 刪除num的末位數字
        		}
        		return res;
        }
        ```
        
    - b進位數字反轉
        
        Time: O(log(n)  / log (b))
        
        Space: O(1)
        
        ```cpp
        int reverse(int num, int b) {
        		int res = 0;
        		while (num > 0) {
        				res = b * res + num % b; // 將末位數字append到res的後面
        				num /= b; // 刪除num的末位數字
        		}
        		return res;
        }
        ```
        
    - 列出num的b進位制
        
        Time: O(log(n)  / log(b))
        
        Space: O(1)
        
        ```cpp
        string toBaseB(int num, int b) {
        		string res = "";
        		while (num > 0) {
        				res = to_string(num % b) + res; // 將末位數字append到res的前面
        				num /= b; // 刪除num的末位數字
        		}
        		if (res == "") return "0"; // num == 0
        		return res;
        }
        ```
        
    
    Leetcode練習：**[1017. Convert to Base -2](https://leetcode.com/problems/convert-to-base-2/)**、[**9. Palindrome Number**](https://leetcode.com/problems/palindrome-number/)、[**2396. Strictly Palindromic Number](https://leetcode.com/problems/strictly-palindromic-number/)、[504. Base 7](https://leetcode.com/problems/base-7/)**
    
4. 附加一個數字 (append a digit after number)
    
    附加 `digit` 到 `number` 後面
    
    ```cpp
    int number;
    int digit; // 0 <= digit <= 9
    number = 10 * number + digit;
    ```
    
    Leetcode練習：[**227. Basic Calculator II**](https://leetcode.com/problems/basic-calculator-ii/)
    
5. 加法進位運算
    
    用carry記錄進位
    
    ```cpp
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0; // 進位
        
        ListNode* p1 = l1;
        ListNode* p2 = l2;
        
        ListNode* dummy = new ListNode(0);
        ListNode* p = dummy;
        
        while (p1 != nullptr || p2 != nullptr || carry != 0) {
            int sum = carry; // 計算當前位數總和
            if (p1 != nullptr) {
                sum += p1->val;
                p1 = p1->next;
            }
            if (p2 != nullptr) {
                sum += p2->val;
                p2 = p2->next;
            }
            
            carry = sum / 10; // 更新carry
            p->next = new ListNode(sum % 10);
            p = p->next;
        }
        
        ListNode* head = dummy->next;
        delete dummy;
        
        return head;
    }
    ```
    
    Leetcode練習：[**2. Add Two Numbers**](https://leetcode.com/problems/add-two-numbers/)、[**67. Add Binary**](https://leetcode.com/problems/add-binary/)
    
6. 指數冪次
    
    判斷n是否為2的冪次：`(n & (n - 1)) == 0`
    
    n如果是2的冪次，其bit可表示成1000…
    
    `n & (n - 1)`是對n做remove lowbit操作
    
    若n為2的冪次，刪除lowbit之後會得到0，反之則不是0
    
    判斷n是否為4的冪次：`(n & (n - 1)) == 0 && (n - 1) % 3 == 0`
    
    n如果是4的冪次，可得到`n = 4^x`
    
    因為`4^x = 2^(2x)`，所以n必為2的冪次，
    
    `n - 1 = 4^x - 1 = 2^(2x) - 1 = (2^x - 1) * (2^x + 1)`
    
    又因為3個連續整數必有一個是3的倍數，所以`(2^x - 1)` 、`2^x`、`(2^x + 1)`之中必有一個是3的倍數
    
    可以知道`2^x`是偶數，所以肯定不是3的倍數，得到`(2^x - 1)` 、`(2^x + 1)`之中必有一個是3的倍數
    
    所以`n - 1 = (2^x - 1) * (2^x + 1)`必然是3的倍數
    
    Leetcode練習：**[231. Power of Two](https://leetcode.com/problems/power-of-two/)、[342. Power of Four](https://leetcode.com/problems/power-of-four/)**
    

### 數列級數

1. 斐波那契數列
    
    $$
    F(0)=0,F(1)=1
    $$
    
    $$
    F(n)=F(n-1)+F(n-2)
    $$
    
    數學解法：
    
    斐波那契數列 `F(n)`是齊次線性遞推，根據遞推方程 `F(n) = F(n - 1) + F(n - 2)`，可以寫出特徵方程：
    
    $$
    x^2=x+1
    $$
    
    求得
    
    $$
    x_1=\frac{1+\sqrt5}{2}, x_2=\frac{1-\sqrt5}{2}
    $$
    
    設通解為
    
    $$
    F(n)=c_1x_1^n+c_2x_2^n
    $$
    
    代入初始條件 `F(0) = 0` , `F(1) = 1`
    
    得到
    
    $$
    c_1=\frac{1}{\sqrt5}, x_2=\frac{-1}{\sqrt5}
    $$
    
    因此斐波那契數的通項公式如下：
    
    $$
    F(n)=\frac{1}{\sqrt5}[(\frac{1+\sqrt5}{2})^n−(\frac{1-\sqrt5}{2})^n]
    $$
    
    得到通項公式之後，就可以通過公式直接求解第 n 項斐波那契數列
    
    Leetcode練習：**[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)、[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)**
    
2. Gray Code
    
    2進位Gray Code鏡射建構法：先列出一組0, 1、再反覆使用鏡射再補1的方法列出Gray Code
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b019f23-0f75-4e97-9ab0-d316f33efcb2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221004%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221004T013538Z&X-Amz-Expires=86400&X-Amz-Signature=0d3c6905c4191dd507ef53f72cb24c79a5c4c1ce0efb12c0dd4c47d7441fb078&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
    
    第 `i` Gray Code：`G(i) = i xor (i >> 1)`
    
    Leetcode練習：**[89. Gray Code](https://leetcode.com/problems/gray-code/)**
    

### 離散數學

1. 因數
    
    完全平方數的因數共有奇數個，其他數字的因數共有偶數個
    
    Leetcode練習：**[319. Bulb Switcher](https://leetcode.com/problems/bulb-switcher/)**
    
2. 判斷數字n是否為質數
    
    檢查2~sqrt(n)之間是否有數字可以整除n
    
    若有數字可以整除n ⇒ 不是質數
    
    沒有數字可以整除n ⇒ 是質數
    
    Time: O(sqrt(n))
    
    Space: O(1)
    
    ```cpp
    bool isPrime(int n) {
        for (int i = 2; i * i <= n; ++i) { // 判斷範圍: 2 ~ sqrt(n)
            if (n % i == 0) return false; // 能整除，不是質數
        }
        return true; // 找不到數可以整除n，是質數
    }
    ```
    
3. 建立質數列表快速判斷n以下的數字是否為質數
    
    ```cpp
    // prime[x]: boolean判斷x是否為質數
    vector<bool> prime(n, true);
    
    // 0和1不是質數
    prime[0] = false; 
    prime[1] = false;
    
    for (int i = 2; i < n; ++i) {
        if (!prime[i]) continue;
        
        for (int j = 2; i * j < n; ++j) {
            prime[i * j] = false; // 質數的倍數都不是質數
        }
    }
    ```
    
    Leetcode練習：[**204. Count Primes**](https://leetcode.com/problems/count-primes/)
    
4. 最大公因數 (gcd)
    
    最大公因數可以用來將一個分數a / b約分到最簡，分子分母同除以gcd(a, b)
    
    Time: O(log(min(a, b)))
    
    Space: O(log(min(a, b)))
    
    ```cpp
    int gcd(int x, int y) {
    		if (y == 0) return x;
    		return gcd(y, x % y);
    }
    ```
    
    Leetcode練習：**[149. Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/)**、**[365. Water and Jug Problem](https://leetcode.com/problems/water-and-jug-problem/)**、**[914. X of a Kind in a Deck of Cards](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/)**、[**2344. Minimum Deletions to Make Array Divisible**](https://leetcode.com/problems/minimum-deletions-to-make-array-divisible/)
    
5. 乘法快速冪求pow(x, n)
    
    Time: O(log(n)), if n is 32-bit integer: O(log(32)) → O(1)
    
    Space: O(log(n)), if n is 32-bit integer: O(log(32)) → O(1)
    
    ```cpp
    int pow(int x, int n) {
        int res = 1;
        while (n > 0) {
            if (n % 2 != 0) res = res * x;
            x = x * x;
            n /= 2;
        }
        return res;
    }
    ```
    
    Leetcode練習：**[50. Pow(x, n)](https://leetcode.com/problems/powx-n/)、[29. Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)**
    
6. 反模元素
    
    方法1：遞迴法
    
    Time: O(a)
    
    Space: O(a)
    
    ```cpp
    long long mod = 1e9 + 7;
    long long inv(long long a) {
        if (a == 1) return 1;
        return (mod - mod / a) * inv(mod % a) % mod;
    }
    ```
    
    方法2：指數法，搭配乘法快速冪
    
    Time: O(log(mod))
    
    Space: O(1)
    
    ```cpp
    long long mod = 1e9 + 7;
    
    long long inv(long long a) {
        return pow(a, mod - 2) % mod;
    }
    
    long long pow(long long x, long long n) {
        long long res = 1;
        while (n > 0) {
            if (n % 2 != 0) res = res * x % mod;
            x = x * x % mod;
            n /= 2;
        }
        return res;
    }
    ```
    
    Leetcode練習：**[1916. Count Ways to Build Rooms in an Ant Colony](https://leetcode.com/problems/count-ways-to-build-rooms-in-an-ant-colony/)**、**[2400. Number of Ways to Reach a Position After Exactly k Steps](https://leetcode.com/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/)**
    

### 排列組合

1. 基本全排列: n!
    
    階乘預處理法
    
    Time: O(n)
    
    Space: O(n)
    
    ```cpp
    vector<int> factorial(n + 1);
    factorial[0] = 1;
    for (int i = 1; i <= n; ++i) {
    		factorial[i] = i * factorial[i - 1];
    }
    ```
    
    Leetcode練習：**[1175. Prime Arrangements](https://leetcode.com/problems/prime-arrangements/)**
    
2. 不重覆組合: C(m, n)
    
    $$
    C_n^m=\frac{m!}{n!(m-n)!}
    $$
    
    “m個不同的物品，取其中的n個物品”的組合方法數
    
    Time: O(min(n, m - n))
    
    Space: O(1)
    
    ```cpp
    int combination(int m, int n) {
        if (n > m) return 0; // n > m, no possible combination
        if (2 * n > m) n = m - n; // choose min(n, m - n)
        if (n == 0) return 1;
        int res = m;
        for (int i = 2; i <= n; ++i) {
            res *= m - i + 1;
            res /= i;
        }
        return res;
    }
    ```
    
    DP法：
    
    $$
    C_n^m=C_{n-1}^{m-1}+C_{n}^{m-1}
    $$
    
    ```cpp
    int mod = 1e9 + 7;
    int combination[1000][1000];
    int combination(int i, int j) {
        if (combination[i][j] != 0) return combination[i][j];
        if (j == 0) return 1;
        if (j == i) return 1;
        
        combination[i][j] = (combination(i - 1, j - 1) + combination(i - 1, j)) % mod;
    
        return combination[i][j];
    }
    ```
    
    Leetcode練習：**[62. Unique Paths](https://leetcode.com/problems/unique-paths/)**
    
3. 不重覆部分排列: P(m, n)
    
    $$
    P_n^m=\frac{m!}{(m-n)!}
    $$
    
    “m個物品，其中有n個物品是相同的”的排列方法數
    
    Time: O(min(n, m - n))
    
    Space: O(1)
    
    ```cpp
    int permutation(int m, int n) {
        if (n > m) return 0; // n > m, no possible permutation
        if (n == 0) return 1;
        int res = 1;
        for (int i = 0; i < n; ++i) {
            res *= m - i;
        }
        return res;
    }
    ```
    
4. 重覆組合: H(m, n)
    
    $$
    H_n^m=C_n^{m+n-1}=\frac{(m+n-1)!}{n!(m-1)!}
    $$
    
    “m位不同的候選人，共n張相同的選票"的組合方法數
    
    使用組合計算重覆組合
    
    Time: O(min(m, n))
    
    Space: O(1)
    
    ```cpp
    int multicombination(int m, int n) {
    		return combination(m + n - 1, n);
    }
    ```
    
5. 重覆排列: m^n
    
    “每次都有m種不同的選擇，共選擇n次”的方法數
    
    用乘法快速冪計算
    
    Time: O(log n), if n is 32-bit integer → O(32) → O(1)
    
    Space: O(1)
    
    ```cpp
    int pow(int m, int n) {
        int res = 1;
        while (n > 0) {
            if (n % 2 != 0) res = res * m;
            m = m * m;
            n /= 2;
        }
        return res;
    }
    ```
    

### 特殊數學題

1. 使用快慢指針找到LinkedList中環的發生位置

使用兩個指針，fast 與slow。它們起始都位於LinkedList的head。隨後，slow 指針每次向後移動1個位置，而 fast 指針向後移動2個位置。如果LinkedList中存在環，則 fast 指針最終將再次與slow指針在環中相遇。

如下圖所示，設LinkedList中環外部分的長度為 a。 slow 指針進入環後，又走了 b 的距離與fast 相遇。此時，fast 指針已經走完了環的 n 圈，因此它走過的總距離為 a + n * (b + c) + b = a + (n + 1) * b + n * c

根據題意，任意時刻，fast 指針走過的距離都為slow 指針的 2 倍。因此，我們有
a + (n+1) * b + n * c = 2 * (a + b) ⟹ a = c + (n − 1) * (b + c)

我們可以發現：從相遇點到入環點的距離加上 n−1 圈的環長，恰好等於從LinkedList head到入環點的距離。

因此，當發現 slow 與 fast 相遇時，我們再額外使用一個指針 ptr。起始，它指向LinkedList head；隨後，它和 slow 每次向後移動一個位置。最終，它們會在入環點相遇。

Time: O(n)

Space: O(1)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ed5971a4-f891-4324-b142-ef7d482b72d0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221004%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221004T013448Z&X-Amz-Expires=86400&X-Amz-Signature=c7f07e7a3644341ec9d67c71792c46a0b1079e9164fff3eb2888a1d0aa94b03f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Leetcode練習：[**142. Linked List Cycle II**](https://leetcode.com/problems/linked-list-cycle-ii/)、**[287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)**