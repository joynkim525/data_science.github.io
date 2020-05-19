---
title: "R tips"
date: 2020-05-19
categories: r
---

* R에서 최빈값 함수 정의하기
```r
getmode <- function(v) {
  uniqv <- unique(v)
  uniqv[which.max(tabulate(match(v, uniqv)))]
}
```
