## Is the difference statistically different?

A 2026 paper titled "Interval cancer, sensitivity, and specificity comparing AI-supported mammography screening with standard double reading without AI in the MASAI study: a randomised, controlled, non-inferiority, single-blinded, population-based, screening-accuracy trial" (<a href="https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(25)02464-X/fulltext">paper link</a>). The paper was published in the Lancet. It reports results from a study involving about 100k women, between April 12, 2021, and Dec 7, 2022, in which these "women were randomly assigned to the intervention or control group. Median age was 53·8 years (IQR 46·5–63·3) in the intervention group and 53·7 years (46·5–63·2) in the control group. Interval cancer rates were 1·55 (95% CI 1·23–1·92) and 1·76 (1·42–2·15) per 1000 participants in the intervention and control group respectively"

A question is: is the difference (1.55 vs 1.76) actually statistically significant (happen not by chance)?

The easiest way to understand the reported p-values is to go back to the **actual counts**, rather than comparing 1.55 and 1.76 directly.

For the MASAI trial, there were:

$n_{AI}=53,043,\qquad x_{AI}=82$

$n_C=52,872,\qquad x_C=93$

giving

$$
p_{AI}=\frac{82}{53043}=0.001546
$$

and

$$
p_C=\frac{93}{52872}=0.001759.
$$

Those become **1.55 and 1.76 interval cancers per 1,000 participants**. ([PubMed][1])

### 1. A simple two-proportion test

Suppose the question is:

$$
H_0:p_{AI}=p_C
$$

versus

$$
H_A:p_{AI}\ne p_C.
$$

Under the null hypothesis, estimate the common probability by pooling the two groups:

$$
\hat p =
\frac{82+93}{53043+52872}
=========================

\frac{175}{105915}
\approx0.001652.
$$

The standard error of the difference is

$$
SE=
\sqrt{
\hat p(1-\hat p)
\left(
\frac{1}{53043}+\frac{1}{52872}
\right)
}
$$

which is approximately

$$
SE\approx0.000250.
$$

The observed difference is

$$
\Delta
======

# 0.001546-0.001759

-0.000213.
$$

Therefore,

$$
z=\frac{-0.000213}{0.000250}\approx-0.85.
$$

For a two-sided test, the p-value is

$$
p=2P(Z>|-0.85|)
$$

which is approximately

$$
\boxed{p\approx0.39}.
$$

So a straightforward two-proportion z-test gives roughly **p = 0.39**, very close to the paper's reported **p = 0.41**.

The small discrepancy arises because the paper's analysis isn't simply this textbook z-test.

### 2. The paper expresses the comparison as a ratio

Instead of emphasizing the difference

$$
1.55-1.76=-0.21,
$$

the authors calculate a **proportion ratio**:

$$
RR=
\frac{82/53043}{93/52872}
\approx0.879.
$$

Hence the reported

$$
\boxed{RR=0.88}.
$$

An RR of 0.88 means the interval-cancer rate in the AI group was about **12% lower**.

For ratios, statistical inference is usually done on the **log scale** because

$$
\log(RR)
$$

is approximately normally distributed.

Here,

$$
\log(0.88)\approx-0.129.
$$

For rare events, a useful approximation to its standard error is

$$
SE[\log(RR)]
\approx
\sqrt{\frac{1}{82}+\frac{1}{93}}
$$

$$
\approx\sqrt{0.01220+0.01075}
\approx0.1515.
$$

So

$$
z\approx\frac{-0.129}{0.1515}
\approx-0.85,
$$

again producing a two-sided p-value around **0.4**.

This is also why the reported 95% CI is fairly wide:

$$
RR=0.88;(95%,CI:0.65-1.18).
$$

Since **1 is inside the confidence interval**, equality between the groups is entirely plausible. The Lancet paper reports **p = 0.41**. ([PubMed][1])

### 3. An intuitive way to understand the p-value

The observed result is approximately:

$$
\boxed{82\text{ cancers versus }93\text{ cancers}}
$$

The question is:

> If AI and conventional screening actually had exactly the same interval-cancer rate, how surprising would it be to randomly get a difference at least this large?

Answer: **not very surprising**.

A difference of 11 cases among approximately 106,000 participants sounds meaningful, but only **175 interval cancers occurred altogether**. Random variation in 175 events is substantial.

That's why:

$$
z\approx-0.85
$$

rather than something like −2 or −3.

A rough rule is that you need

$$
|z|>1.96
$$

for two-sided (p<0.05). Here it is only about 0.85.

### 4. Now compare this with the sensitivity result

This is instructive because the paper reports:

$$
80.5%\quad vs.\quad73.8%,\qquad p=0.031.
$$

The underlying numbers are:

$$
AI:\quad \frac{338}{420}=80.5%
$$

$$
Control:\quad \frac{262}{355}=73.8%.
$$

([Nmgfybjytsg][2])

Now the difference is

$$
80.5%-73.8%=6.7\text{ percentage points}.
$$

The standard error is roughly

$$
SE=
\sqrt{
\frac{0.805(1-0.805)}{420}
+
\frac{0.738(1-0.738)}{355}
}
$$

$$
\approx0.0303.
$$

Therefore,

$$
z\approx
\frac{0.805-0.738}{0.0303}
\approx2.21.
$$

A (z) of about 2.2 corresponds to

$$
\boxed{p\approx0.027}
$$

using this simple approximation, close to the paper's **p = 0.031**.

Again, the slight difference comes from the exact statistical method used by the investigators.

### 5. There's an important issue with the meaning of p = 0.41

This trial was designed as a **non-inferiority trial with a 20% margin**. ([LUP][3])

Therefore, there are actually two different hypotheses one might test.

For **superiority**:

$$
H_0:RR=1
$$

and the observed

$$
RR=0.88
$$

isn't far enough from 1:

$$
\boxed{p=0.41}
$$

so we **cannot claim that AI significantly reduces interval cancers**.

But the primary question was closer to:

$$
H_0:RR\ge1.20
$$

versus

$$
H_A:RR<1.20.
$$

The entire 95% confidence interval was

$$
0.65 < RR < 1.18.
$$

Notice that its upper bound is

$$
\boxed{1.18<1.20}.
$$

Therefore the study could conclude that AI-supported screening was **non-inferior** to conventional double reading. The trial was actually sized around this 20% non-inferiority margin, requiring about 100,000 participants. ([DOI][4])

So the same data support two statements that initially sound contradictory:

$$
\boxed{\text{AI is significantly non-inferior}}
$$

but

$$
\boxed{\text{AI is not significantly superior}}
$$

That's an excellent example for teaching **why a p-value only makes sense after specifying the null hypothesis**. The numbers themselves—1.55 vs. 1.76—don't have a single intrinsic "p-value."

[1]: https://pubmed.ncbi.nlm.nih.gov/41620232/?utm_source=chatgpt.com "Interval cancer, sensitivity, and specificity comparing AI-supported mammography screening with standard double reading without AI in the MASAI study: a randomised, controlled, non-inferiority, single-blinded, population-based, screening-accuracy trial - PubMed"
[2]: https://www.nmgfybjytsg.com/nd.jsp?id=182&utm_source=chatgpt.com "Interval cancer, sensitivity, and specificity comparing AI-supported mammography screening with standard double reading without AI in the - 内蒙古自治区妇幼保健院"
[3]: https://lup.lub.lu.se/search/publication/7851a699-d9c4-4263-93dc-b29779d5b8d4?utm_source=chatgpt.com "Interval cancer, sensitivity, and specificity comparing AI-supported mammography screening with standard double reading without AI in the MASAI study : a randomised, controlled, non-inferiority, single-blinded, population-based, screening-accuracy trial | Lund University Publications"
[4]: https://doi.org/10.1016/s2589-7500%2824%2900267-x?utm_source=chatgpt.com "Screening performance and characteristics of breast cancer detected in the Mammography Screening with Artificial Intelligence trial (MASAI): a randomised, controlled, parallel-group, non-inferiority, single-blinded, screening accuracy study - The Lancet Digital Health"
