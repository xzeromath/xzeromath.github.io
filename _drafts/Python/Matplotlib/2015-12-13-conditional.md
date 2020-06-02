---
# layout: post
title: 조건 수렴하는 수열은 임의로 수렴
categories:
# - Python
# - Math
tags: 
- Math 
- Python
---

## 조건수렴하는 급수는 임의의 값으로 수렴하도록 재배열 할 수 있다.

``` python
import fractions
limit=1000
pl=[1/(2*x-1) for x in range(1,limit)]
mi=[-1/(2*x) for x in range(1,limit)]


goal=-0.5 #수렴값
s=0
i=0
j=0
dis=500 #분모의 최대값
p=0
while p<dis:

    if s>goal:
        s=s+mi[i]
        print(fractions.Fraction(mi[i]).limit_denominator())
        i=i+1

    else:
        s=s+pl[j]
        print(fractions.Fraction(pl[j]).limit_denominator())

        j=j+1

    p=p+1
```
