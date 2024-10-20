# (PART) r基础教程 {-}

# R语言学习路径和资料




## 声明
内容仅为个人学习的经验，并且并不详细。只为方向性引导，大家学习的时候要多在网络上查找资料

## 阶段1：下载好r并使用
1. 先安装最新的[R](https://www.r-project.org/)
2. 再安装IDE
   1. 最常用的IDE就是[Rstudio](https://posit.co/downloads/)
   2. 我目前用的是positron会出一期专门介绍，但是因为还没正式版，有需要的同学可以去看看[更新进展](https://github.com/posit-dev/positron/releases)
3. 了解软件的基本窗口和操作
   1. ![](https://vip.123pan.cn/1813062489//7%20pic/202410192013471.png)

## 阶段2：学习baseR

### 推荐资料

[链接](https://book.douban.com/subject/36420926/)：公认R语言学习最好的书，学习起来清晰通俗，学习路线极其明确

### 学习路线
1. 基础语法：懂得基础的语法知识，安装包，导入包，设定工作路径，使用函数，数据导出
2. **数据结构**：画重点，各个数据结构务必要务必了解。向量还是数据框还是列表，都了解后才能get到后续的列表嵌套数据框和数据框嵌套列表
3. 数据处理：主要处理的对象是数据框，操作包括但不限于变量recode，变量筛选，数据框长宽转换，新建变量，重复值处理
4. 数据可视化：可放单独一块学习，**前期不用学习**
5. 统计分析：可做什么去学什么，**前期不用学**
6. 机器学习（深度学习）：同上

## 阶段3：开始学习tidyverse

### 推荐资料

[R语言编程](https://book.douban.com/subject/36171369/):最好的tidyverse入门书，确实讲的通俗易懂，作者在知乎上有账号，关注不亏

[R数据科学](https://book.douban.com/subject/30277904/)：Hadley Wickham（tidyverse的作者）写的书，讲的很详细，建议细细细细过一遍，获益匪浅

### 学习路径
直接参考加载包的时候的导入函数，一个个学


``` r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

1. 学习数据导入(**readr**)
2. 学习新的数据结构（**tibble**：datafram优化版）
3. 学习数据处理，变量筛选等(**dplyr**)
4. 学习字符变量的处理(**stringr**)
5. 学习因子变量的处理(**forcats**)
6. 学习数据可视化(**ggplot2**)
7. **学习函数式循环（purrr）务必要学**

## 阶段4：学习可视化

### 学习资料

[R数据可视化手册  第2版](http://book.ucdrs.superlib.net/views/specific/2929/bookDetail.jsp?dxNumber=000019332693&d=49173A13F1A674EE50CACCE072F13B33&fenlei=18170403)：系统的看一遍

各大知乎csdn微信公众号关键词搜索：都是宝藏呀

或者来我的[云盘](https://file.wk8686.top/?2%20%E4%BB%A3%E7%A0%81%E6%A8%A1%E6%9D%BF/R)看一看

## 阶段5 统计分析

推荐一个公众号：R语言实战

平时什么统计分析不会全是知乎教我


## 阶段5 机器学习等

mlr3verse包，张敬信大佬可能这两年就会出书介绍

## 阶段6 其他

[rweekly论坛](https://rweekly.org/)

[tidyverse博客](https://www.tidyverse.org/blog/)
