---
title: 中國剩餘定理 不互質
date: 
tags: 
- [整理]
mathjax: true
---
## 題目



- 給你一套方程組如下，其中模數( $k_i$ )不一定互質，求出最小正整數解 $x$ ，如果沒有則輸出 $-1$

$$
\begin{cases}x\equiv p_1\pmod {k_1} \\ x\equiv p_2\pmod {k_2}\\ ......\\ x\equiv p_n\pmod {k_n}\end{cases}
$$

<!-- more -->

## 想法

先以兩兩來看 <br>

$$\begin{cases} x\equiv p_1\pmod {k_1} \\x\equiv p_2\pmod {k_2} \end{cases}$$  <br>

$\Rightarrow \begin{cases} x=k_1x_1+p_1 \tag{1} \\x=k_2x_2+p_2 \end{cases}$  <br>

$k_1x_1+p_1=k_2x_2+p_2$  <br>

$k_1x_1+(-k_2)x_2=p_2-p_1$  <br>

我們下面主要要解的是 $x_1$ 所以跟 $x_2$ 係數的正負沒什麼關西，所以以下都寫正號  <br>

{% note info no-icon %}

### 貝祖定理: 

在 $ax+by=m$ 中，若且唯若 $m$ 是 $a$ 及 $b$ 的最大公因數 $\gcd(a,b)$ 的倍數，有整數解  <br>

{% endnote %}

若 $x_1,x_2$ 有解，則整除 $\gcd(k_1,k_2) \mid p_2-p_1$ ， 如果不是的話代表無解  <br>

令 $\gcd(k_1,k_2)=d$，與 $p_2 - p_1 = c$  <br>

$\Rightarrow \frac{k_1}{d} \times x_1 + \frac{k_2}{d} \times x_2 = \frac{c}{d} \tag{2}$  <br>

其中 $\frac{k_1}{d}$ 與 $\frac{k_2}{d}$ 互質  <br>

{% note info no-icon %} 

### 模逆元移向證明:

$a \times b \equiv c \pmod{m}$  <br>
兩邊同乘 $b^{-1} \Rightarrow a \times (b \times b^{-1}) \equiv c \times b ^{-1} \pmod{m}$  <br>
$a \equiv c \times b^{-1} \pmod{m}$  <br>
{% endnote %}

設 $x^\prime_1$ 為 $\frac{k_1}{d} \times x_1 + \frac{k_2}{d} \times x_2 = 1$ 的解則， $x^\prime_1 \equiv (\frac{k_1}{d})^{-1} \pmod{\frac{k_2}{d}}$ ，這個可以用 extgcd 算出來  <br>
故 $(2)$ 式中 $x_1$ 的解可為 $ansx_1 \equiv \frac{c}{d} \times(\frac{k_1}{d})^{-1} \pmod{\frac{k_2}{d}}$ ( $ansx_1$ 是 $(2)$ 式中 $x_1$ 的解)代回 $(1)$  <br>

$X=k_1 \times ansx_1 + p_1$  <br>
$\Rightarrow X=k_1[\frac{c}{d} \times(\frac{k_1}{d})^{-1}+tmp\times \frac{k_2}{d}]+p_1$  <br>
$\Rightarrow X =k_1\times \frac{c}{d} \times(\frac{k_1}{d})^{-1}+tmp\times \frac{k_1 k_2}{d}+p_1$  <br>
而新的同餘式就是  <br>
$\Rightarrow x \equiv k_1\times\frac{c}{d}\times(\frac{k_1}{d})^{-1}+ p_1 \pmod{\frac{k_1 k_2}{d}}$   <br>
即可表達為 $x \equiv k_1\times ansx_1 + p_1\pmod{\frac{k_1 k_2}{d}}$   <br>
又 $k_1 k_2 = \gcd(k_1,k_2) \times \text{lcm}(k_1,k_2)$ $\Rightarrow \frac{k_1 k_2}{d}= lcm$  <br>
故若得前 $i-1$ 個式子合併得到 $x \equiv X \pmod{lcm}$  <br>
而與第 $i$ 式合併為 $x=ansx_i\times lcm+X \pmod{\frac{lcm\times k_i}{d}}$  <br>

以上面來的 $x=k_1x_1+p_1$ 說，目前的 $k_1=lcm,p_1=X,x_1=ansx_1=ansx_i目前要求的$  <br>

{% note info no-icon %}

### 輾轉相除法:  <br>

$\gcd(a,b)=gcd(b,b \% a)$  <br>
令 $d=\gcd(a,b),a=nd,b=md$  <br>
一直互相相減之後就會得到 $d$  <br>
https://hackmd.io/@Koios/rJ_lER719  <br>
{% endnote %}

{% note info no-icon %}

### 證明: 為什麼除以一個數取模等於乘以這個數的模逆元   <br>

[證明圖片](https://cdn.discordapp.com/attachments/972879937180692551/990257847252160572/unknown.png)  <br>
{% endnote %}

{% note info no-icon %}

### 擴展歐里基德推導:  <br>

$ax+by=\gcd(a,b)$  <br>
$bx_1+(a \% b)y_1=\gcd(a,b)$  <br>
$\Rightarrow ax+by=bx_1+(a-b\times \lfloor{\frac{a}{b}} \rfloor) y_1$  <br>
整理右式 $\Rightarrow ax+by=ay_1+b(x_1 - \lfloor{\frac{a}{b}} \rfloor y_1)$  <br>
推得轉移式 $x=y_1,y=x_1 - \lfloor{\frac{a}{b}} \rfloor y_1$  <br>

```cpp
pii ex_gcd(int a,int b) {
    if (b == 0) {
        return {1, 0};
    }
    pii p = ex_gcd(b, a%b);
    int x = p.second;
    int y = p.first - p.second*(a/b);
    return {x,y};
}
```

{% endnote %}



## 實作

```cpp
#include <bits/stdc++.h> 
#define int long long
#define pii pair<int,int>
using namespace std;

int p[1001], k[1001]; 
int n;

pii ex_gcd(int a,int b) {
    if (b == 0) {
        return {1, 0};
    }
    pii p = ex_gcd(b, a%b);
    int x = p.second;
    int y = p.first - p.second*(a/b);
    return {x,y};
}

int china () {
    int X = p[1];
    int lcm = k[1];

    /*
    x ≡ p1(mod k1)
    x ≡ p2(mod k2)
    x = x1 * k1 + p1
    x = x2 * k2 + p2
    x1 * k1 - x2 * k2 = p2 - p1
    */
    // 可以假設 k1 是已經有的
    // k2 是現在要算的

    for (int i = 2; i <= n; i++) {
        int c = p[i] - X; // p2-p1
        int d = __gcd(k[i], lcm); //k1*k2
        if (c % d != 0) return -1;
        auto [x,y] = ex_gcd(lcm/d, k[i]/d); 
        // (lcm/d)*(x1) + (k2/d)*(x2) = 1
        x = (c) / d * x % (k[i] / d);
        // 因為是模逆元, 被 模過 k[i]*d 下, 要是又超過了就要在模一次
        X += lcm*x; // X 每次都要更新
        lcm = lcm / d * k[i]; // lcm 每次都要更新
        // x ≡ X (mod lcm)
        X %= lcm;
    }
    return (X > 0) ? X  : X + lcm;
}

signed main() {
    while(cin >> n) {
        for (int i = 1; i <= n; i++) {
            cin >> k[i] >> p[i];
        }
        cout << china() << '\n';
    }
        
}

```

credit :  
- [資料1](https://blog.csdn.net/weixin_43602607/article/details/108270977?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165719694016781685328819%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165719694016781685328819&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~sobaiduend~default-3-108270977-null-null.185%5Ev2%5Econtrol&utm_term=%E4%B8%AD%E5%9B%BD%E5%89%A9%E4%BD%99%E5%AE%9A%E7%90%86%20%E4%B8%8D%E4%BA%92%E8%B4%A8&spm=1018.2226.3001.4450)
- [資料2](https://img-blog.csdnimg.cn/20191006130325870.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0MyMDIwMzE0Mw==,size_16,color_FFFFFF,t_70)





## 互質

$\begin{cases}
x\equiv p_1\pmod {k_1} \\
x\equiv p_2\pmod {k_2} \\
\cdots \\
x\equiv p_k\pmod {k_n}
\end{cases}$

- $M = k_1 \times k_2 \times\dots\times k_n$
- $M_i = \frac{M}{k_i}$
- $t_i \equiv M_i^{-1} \pmod {k_i}$
- $X = p_1t_1M_1 + p_2t_2M_2 + \dots +p_nt_nM_n$
- $x=X \pmod{M}$

```cpp
int china () {
    int M = 1;
    for (int i = 1; i <= n; i++) M *= k[i];
    int ret = 0;
    for (int i = 1; i <= n; i++) {
        int Mi = M / k[i];
        auto [t, y] = ex_gcd(Mi, k[i]);
        ret = (ret + p[i]*Mi*t) % M;
        // 最後要去在 1 ~ M 的解, 所以要 mod M
    }
    return (ret + M) % M;
}
```

