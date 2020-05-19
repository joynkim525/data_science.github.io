---
title: "Decision Tree"
date: 2020-05-19 13:16 -0400
categories: r
---

```r
library(C50)

normalize <- function(x){
  return ((x - min(x)) / (max(x) - min(x)))
}
iris_normal <- as.data.frame(lapply(iris[1:4], normalize))
iris_normal$Species <- iris$Species

set.seed(123)
iris_sample <- sample(2, nrow(iris), replace = T, prob = c(0.8, 0.2))
iris_training <- iris_normal[iris_sample == 1, 1:5]
iris_test <- iris_normal[iris_sample == 2, 1:5]

fit <- C5.0(Species ~., data = iris_training, trale = 5)
summary(fit)
plot(fit) 

iris_training[iris_training$Petal.Length > 0.1525424 &
                iris_training$Petal.Length > 0.6610169 &
                iris_training$Petal.Width <= 0.6666667,]
iris_training[iris_training$Petal.Length > 0.1525424 &
                iris_training$Petal.Length > 0.66101695 &
                iris_training$Petal.Width <= 0.6666667,]
                
norm <- function(x){
  return (round((x - min(x)) / (max(x) - min(x)), 5))
}
iris_norm <- as.data.frame(lapply(iris[1:4], norm))
iris_norm$Species <- iris$Species

iris_sample <- sample(2, nrow(iris), replace = T, prob = c(0.8, 0.2))
iris_training <- iris_normal[iris_sample == 1, 1:5]
iris_test <- iris_normal[iris_sample == 2, 1:5]

fit <- C5.0(Species ~., data = iris_training, trale = 5)
summary(fit)
plot(fit) 
```

데이터를 normalize를 진행한 다음에 Decision Tree를 적용시켜보면, <br>
summary로 나오는 분류 결과와 plot에서 나타나는 결과가 다른 경우가 있다. <br>
이러한 오류가 나타나는 이유는 normalize를 하는 과정에서 실제로는 소수점 자리가 매우 긴데, <br>
화면 상에는 7자리밖에 표현되지 않아서 plot에 입력값이 다르게 들어가면서 발생한다. <br>
예를 들어 소수점 자리 10자리쯤에서 가지가 나뉘는데, plot에는 소수점 자리 7자리까지만 입력값으로 들어가는 셈이다. <br>
이러한 오류를 미리 방지하기 위해서는 미리 round를 통해 소수점 자리를 정리해놓는 것이 좋을 듯하다.
