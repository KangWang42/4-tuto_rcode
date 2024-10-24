# purrr: 函数式编程,彻底摆脱for循环




## R包介绍

purrr 通过提供一套完整且一致的用于处理函数和向量的工具来增强 **R 的函数式编程 (FP) 工具包**。如果您以前从未听说过 FP，那么最好的起点是map()函数系列，它允许您用更简洁、更易于阅读的代码替换许多 for 循环。

听起来有点复杂，但更简单来说，就是用嵌套函数来**替代for循环的冗长的框架结构**。让输入输出更简单。

相关教程：[官网网站](https://purrr.tidyverse.org/)

## R包安装



``` r
install.packages("purrr")
```

## 语法

purrr系列函数都以**map，map2和pmap作为大类，搭配更多的后缀来设定输出类型**。

- map(.x, .f)：输入一个向量(.x)，以该向量为输入进行循环(.f函数循环)
- map(.x, .f)：输入两个向量
- map3(.x, .f)：输入n（大于2）向量

这里边的向量是比较广的向量，包含**向量，列表，字符串，数据框（可以看作向量的向量），只要有这种顺序结构的都可以作为map的输入**


## 举个栗子

### 加载数据

``` r
library(tidyverse)
library(purrr)
```


``` r
data <- mtcars

head(data, 5)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
```

### 使用tidyverse结构和purrr来划分数据分别做回归

我们现在想根据cyl对数据框进行划分，在分出来的数据框中做回归，然后把回归结果放到一个数字向量里


``` r
data |> 
  split(data$cyl) |>  # 划分数据
  map(\(df) lm(mpg ~ wt, data = df)) |> #分别做循环
  map(summary) %>%  #对结果做summary
  map_dbl("r.squared")
```

```
##         4         6         8 
## 0.5086326 0.4645102 0.4229655
```

查看以下代码，发现了什么？

- purrr循环的第一个参数始终是数据，因此 purrr 可以自然地与管道配合使用。
- map_xxx（map的后缀相当于自定义了输出类型）

### 常规方法来做这个模型


``` r
var <- c("disp", "hp", "drat")

data_list <- split(data, mtcars$cyl)

vec_result = c()
for (temp_data in data_list) {
    model = lm(mpg ~ wt, data = temp_data)
    model_summary = summary(model)
    r2 = model_summary$"r.squared"
    vec_result = c(vec_result, r2)
}

print(vec_result)
```

```
## [1] 0.5086326 0.4645102 0.4229655
```

发现了什么

1. 代码行数多了很多
2. 多了一些中间变量
3. 代码可读性差，很不优雅

## 多变量索引循环

如果是想用多个向量来索引循环，输入多个向量，我们要怎么做呢。举一个简单的例子就知道了。


``` r
var1 <- c("disp", "hp", "drat")
var2 <- c("wt", "qsec", "vs")
var_add <- map2(var1, var2, \(x, y) paste0(x, "+", y))
print(var_add)
```

```
## [[1]]
## [1] "disp+wt"
## 
## [[2]]
## [1] "hp+qsec"
## 
## [[3]]
## [1] "drat+vs"
```

再举个例子


``` r
means <- 1:4
sds <- 1:4
set.seed(2020)
samples <- map2(means, sds, \(mean, sds){rnorm(mean, sds, n = 5)})

#这里也可以写为，如下，不过有时候想要更复杂的操作就不要用这种简化的写法
#samples <- map2(means, sds, rnorm, n = 5)
str(samples)
```

```
## List of 4
##  $ : num [1:5] 1.377 1.302 -0.098 -0.13 -1.797
##  $ : num [1:5] 3.44 3.88 1.54 5.52 2.23
##  $ : num [1:5] 0.441 5.728 6.589 1.885 2.63
##  $ : num [1:5] 11.2 10.82 -8.16 -5.16 4.23
```

如果输入的是多个向量可以参考如下


``` r
var3 <- c("disp", "hp", "drat")

var4 <- c("wt", "qsec", "vs")

#使用pmap的时候，把多个向量放到list框里作为第一个参数
pvar_add <- pmap(list(var1, var2, var3, var4), 
            \(x, y, z, p) 
            paste0(x, "+", y, "+", z, "+", "p"))

print(pvar_add)
```

```
## [[1]]
## [1] "disp+wt+disp+p"
## 
## [[2]]
## [1] "hp+qsec+hp+p"
## 
## [[3]]
## [1] "drat+vs+drat+p"
```

注意：这里用的都是简单的字符向量，但我们使用的时候可以自由拓展到数据框和列表等复杂向量结构，就能感觉到purrr循环的魅力了



## 嵌套循环

如果是嵌套结构我们怎么用purrr来做呢，其实也很简单。我们现在来算一下1：10分别乘以10:20然后放到一个数字向量里怎么实现吧


``` r
map(1:10, 
        \(x){map(10:20, 
        \(y){x*y})}) |> 
    unlist()
```

```
##   [1]  10  11  12  13  14  15  16  17  18  19  20  20  22  24  26  28  30  32
##  [19]  34  36  38  40  30  33  36  39  42  45  48  51  54  57  60  40  44  48
##  [37]  52  56  60  64  68  72  76  80  50  55  60  65  70  75  80  85  90  95
##  [55] 100  60  66  72  78  84  90  96 102 108 114 120  70  77  84  91  98 105
##  [73] 112 119 126 133 140  80  88  96 104 112 120 128 136 144 152 160  90  99
##  [91] 108 117 126 135 144 153 162 171 180 100 110 120 130 140 150 160 170 180
## [109] 190 200
```

举得例子比较没有意义，但是可以在此基础上一窥嵌套循环的实现。

## 更多

purrr可以快捷实现很多高级操作，比如批量导入数据，批量绘图以及批量建模等，后续分开写吧。这一期写得很宽泛，大家可以自己去探索更多操作。