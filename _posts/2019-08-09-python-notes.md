---
layout: post
title:  "Python笔记"
date:   2019-08-09 01:14:00 +0800
author: Mermaid
categories: technical
---
按：本文是Mermaid在使用Python进行数据处理时的学习笔记，经授权发表于此。

<!-- Some notes of Python Learning -->
<!-- Credit to Mermaid -->

## Datetime Package
> 2019.08.07, Wed, Beijing

`datetime` 为一种专门储存日期、时间的数据类型，可用于日期/时间的快速访问、格式转换、加减计算等。

-   加载
    ```
    import time
    from datetime import datetime, timedelta
    ```

-   构建
    ```
    datetime(year, month, day, hr, min, sec)

    # read from string
    datetime.strptime(str, '%Y-%m-%d %H:%M:%S')
    ```
-   计算时间差：支持直接加减乘除计算

    ```
    # start_time = 2019-05-24 08:05:33
    # end_time = 2019-05-24 08:30:59

    duration = end_time - start_time
    print(duration)

    # duration = 0:25:26
    ```

-   获取总秒数

    ```
    duration.total_seconds()

    # 1526.0
    ```

更多函数详见 [Python Standard Library](https://docs.python.org/3.7/library/datetime.html)


## Pandas csv read and write
> 2019.08.08, Thu, Beijing

-   package

    ```
    import pandas
    import os
    ```

-   read path

    ```
    files = os.listdir(folder)
    ```

-   指定后缀名
  
    ```
    for file in files:
        if os.path.splitext(file)[1] == '.csv':
            XXXXX actions

    # splitext分离文件名与扩展名
    ```

-   read csv

    ```
    df = pd.read_csv(path+name)
    ```

-   write csv



## Pandas dataframe
> 2019.08.08, Thu, Beijing

dataframe是pandas包的数据结构。这里记录使用时遇到的一些问题

-   数据清洗时，del部分行之后index不更新，导致循秩访问失败（主要是循环）
    -   解决方法：重置index
  
        ```
        df = df.reset_index(drop = True) 
        % drop = True是为了把原来的idx列删去
        ```

-   对列做运算
    -   单列运算：按秩循环运算非常慢，比直接对list操作或map函数慢不止一两个数量级。直接按元素循环也比按秩循环快。因此实际操作时能用map尽量用map，或许在执行原理上直接整体操作了。
    -   example of map function 
 
        ```
        df['col1'] = df['col2'].map(definedFunc)
        df['col1'] = df['col2'].map(lambda x : x ** 2)
        ```

-   查找字符串问题
    -   两个df有相同的uuid（字段，column），想通过这个共同字段进行匹配，把第二个df中的其他信息匹配至第一个df。但是如果直接适用df进行‘==’查找，效率非常低，是O(n)的速度。
    -   解决方案：把被查找的df转变为dict，把uuid设置为key，这样就可以直接按key访问，复杂度降为O(log n)，速度变快超级多（由1天+变为5秒）

        ```
        dict = df.set_index('colomn').T.to_dict('list')
        ```
