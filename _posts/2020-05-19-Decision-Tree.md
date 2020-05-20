---
title: "Decision Tree"
date: 2020-05-19 13:16 -0400
categories: r
---

```r
library(C50)

normalize <- function(x){
  return ((x - min(x)) / (max(x) - min(x)))
} # define normalize function
iris_normal <- as.data.frame(lapply(iris[1:4], normalize))
iris_normal$Species <- iris$Species
```


```r
set.seed(123)
iris_sample <- sample(2, nrow(iris), replace = T, prob = c(0.8, 0.2))
iris_training <- iris_normal[iris_sample == 1, 1:5]
iris_test <- iris_normal[iris_sample == 2, 1:5]
```

```r
fit <- C5.0(Species ~., data = iris_training, trale = 5)
summary(fit)

Call:
C5.0.formula(formula = Species ~ ., data = iris_training, trale = 5)


C5.0 [Release 2.07 GPL Edition]  	Wed May 20 10:49:46 2020
-------------------------------

Class specified by attribute `outcome'

Read 121 cases (5 attributes) from undefined.data

Decision tree:

Petal.Length <= 0.1525424: setosa (39)
Petal.Length > 0.1525424:
:...Petal.Width > 0.6666667: virginica (36/1)
    Petal.Width <= 0.6666667:
    :...Petal.Length <= 0.6610169: versicolor (40)
        Petal.Length > 0.6610169: virginica (6/2)


Evaluation on training data (121 cases):

	    Decision Tree   
	  ----------------  
	  Size      Errors  

	     4    3( 2.5%)   <<


	   (a)   (b)   (c)    <-classified as
	  ----  ----  ----
	    39                (a): class setosa
	          40     3    (b): class versicolor
	                39    (c): class virginica


	Attribute usage:

	100.00%	Petal.Length
	 67.77%	Petal.Width


Time: 0.0 secs

plot(fit) 


```

```r
iris_training[iris_training$Petal.Length > 0.1525424 &
                iris_training$Petal.Length > 0.6610169 &
                iris_training$Petal.Width <= 0.6666667,]
                
    Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
53     0.7222222  0.45833333    0.6610169   0.5833333 versicolor
73     0.5555556  0.20833333    0.6610169   0.5833333 versicolor
78     0.6666667  0.41666667    0.6779661   0.6666667 versicolor
84     0.4722222  0.29166667    0.6949153   0.6250000 versicolor
120    0.4722222  0.08333333    0.6779661   0.5833333  virginica
130    0.8055556  0.41666667    0.8135593   0.6250000  virginica
134    0.5555556  0.33333333    0.6949153   0.5833333  virginica
135    0.5000000  0.25000000    0.7796610   0.5416667  virginica

iris_training[iris_training$Petal.Length > 0.1525424 &
                iris_training$Petal.Length > 0.66101695 &
                iris_training$Petal.Width <= 0.6666667,]

    Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
78     0.6666667  0.41666667    0.6779661   0.6666667 versicolor
84     0.4722222  0.29166667    0.6949153   0.6250000 versicolor
120    0.4722222  0.08333333    0.6779661   0.5833333  virginica
130    0.8055556  0.41666667    0.8135593   0.6250000  virginica
134    0.5555556  0.33333333    0.6949153   0.5833333  virginica
135    0.5000000  0.25000000    0.7796610   0.5416667  virginica
```

```r
norm <- function(x){
  return (round((x - min(x)) / (max(x) - min(x)), 5))
}
iris_norm <- as.data.frame(lapply(iris[1:4], norm))
iris_norm$Species <- iris$Species

iris_sample <- sample(2, nrow(iris), replace = T, prob = c(0.8, 0.2))
iris_training <- iris_normal[iris_sample == 1, 1:5]
iris_test <- iris_normal[iris_sample == 2, 1:5]
```

```r
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
