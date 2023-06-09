# 数据库:解释数据规范化、数据异常和 DBMS 键

> 原文：<https://towardsdatascience.com/softly-explained-data-normalization-data-anomalies-and-dbms-keys-f8122aefaeb3?source=collection_archive---------3----------------------->

## 数据科学工程

![](img/d9889d6c3c01357c15e18307fd5becc4.png)

这篇文章将对数据库规范化和它的其他方面做一个简短的解释。俗话说，“人无完人！”我也不例外，所以请随时评论我可能犯的任何错误。

*注意:数据库的领域是巨大的，基于这篇文章不应该被低估。*

我们需要规范化是为了什么？要解决这些问题:

# 反常

**1-** **更新异常**:假设我们在一个表格中有 10 列，其中 2 列称为员工姓名和员工地址。现在，如果一名员工改变了位置，我们就必须更新该表。但问题是，如果表没有被规范化，一个雇员可能有多个条目，当更新所有这些条目时，其中一个可能会丢失。

2-插入异常:假设我们有一个有 4 列的表。学号，学名，学生地址，学生成绩。现在，当一个新生入学时，即使前三个属性可以填写，但第四个属性将为空值，因为他还没有任何分数。

**3-删除异常**:该异常表示从表格中删除了不必要的重要信息。假设我们有学生的信息和他们参加的课程，如下所示(学生 ID、学生姓名、课程、地址)。如果任何学生离开学校，那么与该学生相关的条目将被删除。但是，即使课程取决于学校而不是学生，删除操作也会删除课程信息。

规范化试图将表细化到可以避免这些问题的状态。简而言之，它试图将表分成多个表，并使用键定义它们之间的关系。

# 重要的钥匙

**a)主键**:这个键唯一地标识表中每个条目。该值不能在表中重复，并且不能包含空值。通常第一列被定义为主键。示例(学号)。

**b)外键:**该键可以有重复的值，但是为了唯一地标识每个条目，该表仍然可以有独立于外键列的主键列。但是，外键将创建与另一个表的关系，在该表中，这些值被定义为主键。

**c)复合键**:这是定义多列为主键的方法。在表中没有列具有唯一值的情况下，我们可以将两列或两列以上的组合定义为唯一的，并将其设置为主键。例如:(学生姓名、地址、分数等。)在这里，学生可能有相同的名字，因此我们将学生名字和地址的组合定义为主键。现在更不可能有同名同姓的学生了。

**d)候选键**:简单的说，候选键是一个键，也可以作为主键。例如:(学生证，学生证号，地址，标记)这里学生证是主键，因为它没有重复值，没有空值。然而，学生卷号还包含主键的所有属性，因此被视为候选键。

**f)代理键**:这意味着当没有其他列能够保存主键的属性时，人工创建的唯一标识表中每个条目的值。它是一个附加列，通常保存整数值。

请记住，我们不能对主键在另一个表中作为外键的表进行任何更改。换句话说，如果主键被另一个表中的外键引用，我们就不能对它进行更改。或者说，如果父表有一个外键引用父表的主键的子表，我们就不能对其主键进行更改。

# 正常化

1NF:第一个范式表示表格的每个单元格必须只有一个值。因此，行和列的每个交集必须包含原子值。例如:如果我们有一个列名 phone_number，则该列的每一行必须只保存一个电话号码。

2NF:我们在上面看到了候选人密钥，这就是它的作用。2NF 规则表示表中没有非质数属性依赖于任何候选键。简而言之，如果表代表两个不同的实体，那么它应该被分解成它们自己的实体。例如:如果我们有一个表(学生 ID、学生姓名、课程编号、课程名称、教师 ID、教师姓名)，它表示由学校每位教师讲授的每门课程中注册的每个学生的信息。由于它代表了三种不同的实体，因此必须将其标准化为 2NF 形式。

3NF:此规则表示表必须是 2NF 形式，并且每个表应该只包含非过渡依赖于自己表的主键的列。简单地说，如果我们有一个表(交易 ID，价格，数量，total_sales)，这里的总销售额是价格和数量(价格*数量)的乘积。因此，销售过渡依赖于交易标识，这是这里的一个主键。所以每个属性必须直接依赖于主键。