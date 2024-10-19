# R包推荐-bruceR-r包里的瑞士军刀



## r包介绍

[使用教程](https://zhuanlan.zhihu.com/p/281150493)

作者在日常工作中集各常用包于大成，凝结出了bruceR，很多内容都是专门为科研而生，减少了很多工作

可以实现以下功能！星标一看！安装即用

- 设置路径
- 数据打印和三线表制作
- 数据编码
- 数据框的横向计算
- 一致性检验
- 探索性因子分析
- 验证性因子分析
- 描述统计
- 统计结果summary
- 结构方程模型
- 等等等

## r包安装

CRAN直接安装

或者 github库安装


``` r
install.packages("devtools")
devtools::install_github("psychbruce/bruceR", dep=TRUE, force=TRUE)
```

## 基础使用



``` r
#install.packages("bruceR")
library("bruceR")
```

```
## 
## bruceR (v2024.6)
## Broadly Useful Convenient and Efficient R functions
## 
## Packages also loaded:
## ✔ data.table	✔ emmeans
## ✔ dplyr     	✔ lmerTest
## ✔ tidyr     	✔ effectsize
## ✔ stringr   	✔ performance
## ✔ ggplot2   	✔ interactions
## 
## Main functions of `bruceR`:
## cc()          	Describe() 	TTEST()
## add()         	Freq()     	MANOVA()
## .mean()       	Corr()     	EMMEANS()
## set.wd()      	Alpha()    	PROCESS()
## import()      	EFA()      	model_summary()
## print_table() 	CFA()      	lavaan_summary()
## 
## For full functionality, please install all dependencies:
## install.packages("bruceR", dep=TRUE)
## 
## Online documentation:
## https://psychbruce.github.io/bruceR
## 
## To use this package in publications, please cite:
## Bao, H.-W.-S. (2024). bruceR: Broadly useful convenient and efficient R functions (Version 2024.6) [Computer software]. https://CRAN.R-project.org/package=bruceR
```

### set_wd:设置工作路径

快速将当前r文档路径设为工作路径


``` r
set_wd()
```

### import:一个函数导入或导出各种数据

import函数支持但不限于几乎常用数据库的导入
- 文本格式 txt, .csv, .csv2, .tsv, .psv 
- Excel (.xls, .xlsx)
- SPSS (.sav)
- Stata (.dta)
- R objects (.rda, .rdata, .RData)
- R serialized objects (.rds)
- Clipboard（on Windows and Mac OS）

### print_table：快速生成三线表


``` r
print_table(npk)
```

```
## ──────────────────────
##     block N P K  yield
## ──────────────────────
## 1       1 0 1 1 49.500
## 2       1 1 1 0 62.800
## 3       1 0 0 0 46.800
## 4       1 1 0 1 57.000
## 5       2 1 0 0 59.800
## 6       2 1 1 1 58.500
## 7       2 0 0 1 55.500
## 8       2 0 1 0 56.000
## 9       3 0 1 0 62.800
## 10      3 1 1 1 55.800
## 11      3 1 0 0 69.500
## 12      3 0 0 1 55.000
## 13      4 1 0 0 62.000
## 14      4 1 1 1 48.800
## 15      4 0 0 1 45.500
## 16      4 0 1 0 44.200
## 17      5 1 1 0 52.000
## 18      5 0 0 0 51.500
## 19      5 1 0 1 49.800
## 20      5 0 1 1 48.800
## 21      6 1 0 1 57.200
## 22      6 1 1 0 59.000
## 23      6 0 1 1 53.200
## 24      6 0 0 0 56.000
## ──────────────────────
```

``` r
#设置导出到doc中
#print_table(npk, file="")
```

### model_summary：常用模型结果summary

bruceR的model_summary可以对常见的线性非线性，生存分析，结构方程模型等整洁化结果输出。快速生成美观的结果，通过file参数导出到doc文件里


``` r
head(airquality, 5)
```

```
##   Ozone Solar.R Wind Temp Month Day
## 1    41     190  7.4   67     5   1
## 2    36     118  8.0   72     5   2
## 3    12     149 12.6   74     5   3
## 4    18     313 11.5   62     5   4
## 5    NA      NA 14.3   56     5   5
```

``` r
airquality %>% 
  lm(Temp ~ Month + Day + Wind + Solar.R,data=.)%>% 
  model_summary()
```

```
## 
## Model Summary
## 
## ────────────────────────
##              (1) Temp   
## ────────────────────────
## (Intercept)   68.770 ***
##               (4.391)   
## Month          2.225 ***
##               (0.441)   
## Day           -0.084    
##               (0.070)   
## Wind          -1.003 ***
##               (0.176)   
## Solar.R        0.027 ***
##               (0.007)   
## ────────────────────────
## R^2            0.387    
## Adj. R^2       0.369    
## Num. obs.    146        
## ────────────────────────
## Note. * p < .05, ** p < .01, *** p < .001.
## 
## # Check for Multicollinearity
## 
## Low Correlation
## 
##     Term  VIF    VIF 95% CI Increased SE Tolerance Tolerance 95% CI
##    Month 1.03 [1.00,  4.91]         1.02      0.97     [0.20, 1.00]
##      Day 1.02 [1.00, 22.58]         1.01      0.98     [0.04, 1.00]
##     Wind 1.03 [1.00,  6.15]         1.02      0.97     [0.16, 1.00]
##  Solar.R 1.03 [1.00,  5.32]         1.02      0.97     [0.19, 1.00]
```

### RECODE:recode重新编码

示例用的是datatable包，这个比较难暂时可以不用管


``` r
d = data.table(var=c(NA, 0, 1, 2, 3, 4, 5, 6))
d
```

```
##      var
##    <num>
## 1:    NA
## 2:     0
## 3:     1
## 4:     2
## 5:     3
## 6:     4
## 7:     5
## 8:     6
```

``` r
d[, `:=`(
  var.new = RECODE(var, "lo:1=0; c(2,3)=1; 4=2; 5:hi=3; else=999")
)]
d
```

```
##      var var.new
##    <num>   <num>
## 1:    NA     999
## 2:     0       0
## 3:     1       0
## 4:     2       1
## 5:     3       1
## 6:     4       2
## 7:     5       3
## 8:     6       3
```



## 其它函数

作者应该是把日常能汇总的都汇总到了一起，函数太多了，方法面面都会用到

建议大家可以去作者 包寒吴霜 的知乎主页里学习一番，对r语言的提高大有裨益
