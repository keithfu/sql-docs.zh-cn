---
title: "DBCC SHOW_STATISTICS (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHOW_STATISTICS_TSQL
- DBCC SHOW_STATISTICS
- SHOW_STATISTICS
- DBCC_SHOW_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], densities
- histograms [SQL Server]
- statistical information [SQL Server], viewing statistics objects
- current distribution statistics
- query optimization statistics [SQL Server], histograms
- DBCC SHOW_STATISTICS statement
- distribution statistics
- statistical information [SQL Server], densities
- statistics objects
- statistical information [SQL Server], histograms
- query optimization statistics [SQL Server], viewing statistics objects
- statistical information [SQL Server], distribution
- densities [SQL Server]
- displaying distribution statistics
ms.assetid: 12be2923-7289-4150-b497-f17e76a50b2e
caps.latest.revision: 75
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 03651b89f8cc8b7694e9e07531804053e64568ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-showstatistics-transact-sql"></a>DBCC SHOW_STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

DBCC SHOW_STATISTICS 显示表或索引视图的当前查询优化统计信息。 查询优化器使用统计信息估计查询结果中的基数或行数，这样，查询优化器可以创建高质量的查询计划。 例如，查询优化器可以使用基数估计在查询计划中选择索引查找运算符而不是索引扫描运算符，从而通过避免消耗大量资源的索引扫描来提高查询性能。
  
查询优化器将表或索引视图的统计信息存储在统计信息对象中。 对于表，统计信息对象是根据索引或表列的列表创建的。 统计信息对象在统计信息对象和密度向量来测量跨列相关性的第一个键列中包含有关统计信息的元数据具有的标头，与值分布的直方图。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]可以使用统计信息对象中的任何数据计算基数估计。
  
DBCC SHOW_STATISTICS 根据统计信息对象中存储的数据显示标题、直方图和密度向量。 使用以下语法，您可以指定表或索引视图以及目标索引名称、统计信息名称或列名。 本主题说明如何显示统计信息以及如何理解显示的结果。
  
有关更多信息，请参见 [Statistics](../../relational-databases/statistics/statistics.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```
-- Syntax for SQL Server and Azure SQL Database  
  
DBCC SHOW_STATISTICS ( table_or_indexed_view_name , target )   
[ WITH [ NO_INFOMSGS ] < option > [ , n ] ]  
< option > :: =  
    STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM  
```  
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

DBCC SHOW_STATISTICS ( table_name , target )   
    [ WITH {STAT_HEADER | DENSITY_VECTOR | HISTOGRAM } [ ,...n ] ]  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *table_or_indexed_view_name*  
 要显示其统计信息的表或索引视图的名称。  
  
 *table_name*  
 包含要显示的统计信息的表的名称。 表不能为外部表。  
  
 *目标 (target)*  
 要显示其统计信息的索引、统计信息或列的名称。 *目标*括在方括号内，单个引号、 double 引号或没有引号。 如果*目标*是现有索引的名称或返回对表或索引的视图，此目标有关的统计信息的统计信息。 如果*目标*是某个现有列的名称，以及在该列上的自动创建统计信息是否存在，则返回该自动创建的统计信息有关的信息。 如果列目标中不存在自动创建的统计信息，则返回错误消息 2767。  
 在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，*目标*不能为列名称。  
  
 NO_INFOMSGS  
 取消严重级别从 0 到 10 的所有信息性消息。  
  
 STAT_HEADER |DENSITY_VECTOR |直方图 |STATS_STREAM [ **，**  *n*  ]  
 如果指定以上一个或多个选项，将根据指定的选项限制该语句返回的结果集。 如果没有指定任何选项，则返回所有统计信息。  
  
 STATS_STREAM 为 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>结果集  
下表对指定 STAT_HEADER 时结果集中所返回的列进行了说明。
  
|列名|Description|  
|-----------------|-----------------|  
|Name|统计信息对象的名称。|  
|Updated|上一次更新统计信息的日期和时间。 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md)函数是另一种方法检索此信息。|  
|行|上次更新统计信息时表或索引视图中的总行数。 如果筛选统计信息或者统计信息与筛选索引对应，该行数可能小于表中的行数。 有关详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。|  
|Rows Sampled|用于统计信息计算的抽样总行数。 如果 Rows Sampled < Rows，显示的直方图和密度结果则是根据抽样行估计的。|  
|步骤|直方图中的梯级数。 每个梯级都跨越一个列值范围，后跟上限列值。 直方图梯级是根据统计信息中的第一个键列定义的。 最大梯级数为 200。|  
|Density|计算公式为 1/统计信息对象第一个键列中的所有值（不包括直方图边界值）的非重复值。 查询优化器不使用此 Density 值，显示此值的目的是为了与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的版本实现向后兼容。|  
|Average Key Length|统计信息对象中所有键列的每个值的平均字节数。|  
|String Index|Yes 指示统计信息对象包含字符串摘要统计信息，以改进对使用 LIKE 运算符的查询谓词的基数估计；例如 `WHERE ProductName LIKE '%Bike'`。 字符串摘要统计信息与直方图分开存储，并当它是类型的统计信息对象第一个键列上创建**char**， **varchar**， **nchar**， **nvarchar**， **varchar （max)**， **nvarchar (max)**，**文本**，或**ntext。**。|  
|筛选表达式|包含在统计信息对象中的表行子集的谓词。 NULL = 未筛选的统计信息。 有关筛选的谓词的详细信息，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。 有关筛选的统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。|  
|Unfiltered Rows|应用筛选表达式前表中的总行数。 如果筛选表达式为 NULL，则 Unfiltered Rows 等于 Rows。|  
|保留示例百分比|保留用于未显式指定抽样百分比的统计信息更新的示例百分比。 如果值为零，则无持久化的示例百分比设置为此统计信息。<br /><br /> **适用于：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4| 
  
下表对指定 DENSITY_VECTOR 时结果集中所返回的列进行了说明。
  
|列名|Description|  
|-----------------|-----------------|  
|All Density|密度为 1/非重复值。 结果显示统计信息对象中各列的每个前缀的密度，每个密度显示一行。 非重复值是每个行前缀和列前缀的列值的非重复列表。 例如，如果统计信息对象包含键列 (A, B, C)，结果将报告以下每个列前缀中非重复值列表的密度：(A)、(A,B) 以及 (A, B, C)。 使用前缀 (A, B, C)，以下每个列表都是一个非重复值列表：(3, 5, 6)、(4, 4, 6)、(4, 5, 6) 和 (4, 5, 7)。 使用前缀 (A, B)，相同列值则具有以下非重复值列表：(3, 5)、(4, 4) 和 (4, 5)|  
|Average Length|存储列前缀的列值列表的平均长度（以字节为单位）。 例如，如果列表 (3, 5, 6) 中的每个值都需要 4 个字节，则长度为 12 个字节。|  
|列|为其显示 All density 和 Average length 的前缀中的列的名称。|  
  
下表对指定 HISTOGRAM 选项时结果集中所返回的列进行了说明。
  
|列名|Description|  
|---|---|
|RANGE_HI_KEY|直方图梯级的上限列值。 列值也称为键值。|  
|RANGE_ROWS|其列值位于直方图梯级内（不包括上限）的行的估算数目。|  
|EQ_ROWS|其列值等于直方图梯级的上限的行的估算数目。|  
|DISTINCT_RANGE_ROWS|非重复列值位于直方图梯级内（不包括上限）的行的估算数目。|  
|AVG_RANGE_ROWS|重复列值位于直方图梯级内（不包括上限）的平均行数（如果 DISTINCT_RANGE_ROWS > 0，则为 RANGE_ROWS / DISTINCT_RANGE_ROWS）。| 
  
## <a name="remarks"></a>注释  
  
## <a name="histogram"></a>直方图  
直方图度量数据集中每个非重复值的出现频率。 查询优化器根据统计信息对象第一个键列中的列值来计算直方图，它选择列值的方法是以统计方式对行进行抽样或对表或视图中的所有行执行完全扫描。 如果直方图是根据一组抽样行创建的，存储的总行数和非重复值总数则为估计值，且不必为整数。
  
若要创建直方图，查询优化器将对列值进行排序，计算与每个非重复列值匹配的值数，然后将列值聚合到最多 200 个连续直方图梯级中。 每个梯级都包含一个列值范围，后跟上限列值。 该范围包括介于两个边界值之间的所有可能列值，但不包括边界值自身。 最小排序列值是第一个直方图梯级的上限值。
  
下面的关系图显示包含六个梯级的直方图。 第一个上限值左侧的区域是第一个梯级。
  
![](../../relational-databases/system-dynamic-management-views/media/a0ce6714-01f4-4943-a083-8cbd2d6f617a.gif "a0ce6714-01f4-4943-a083-8cbd2d6f617a")
  
对于每个直方图梯级：
-   粗线表示上限值 (RANGE_HI_KEY) 和上限值的出现次数 (EQ_ROWS)  
-   RANGE_HI_KEY 左侧的纯色区域表示列值范围和每个列值的平均出现次数 (AVG_RANGE_ROWS)。 第一个直方图梯级的 AVG_RANGE_ROWS 始终是 0。  
-   点线表示用于估计范围中的非重复值总数 (DISTINCT_RANGE_ROWS) 和范围中的总值数 (RANGE_ROWS) 的抽样值。 查询优化器使用 RANGE_ROWS 和 DISTINCT_RANGE_ROWS 计算 AVG_RANGE_ROWS，且不存储抽样值。  
  
查询优化器按照直方图梯级的统计重要性来定义直方图梯级。 它使用最大差异算法使直方图中的梯级减至最少，并同时最大化边界值之间的差异。 最大梯级数为 200。 直方图梯级数可以少于非重复值的数目，即使对于边界点少于 200 的列也是如此。 例如，具有 100 个非重复值的列所具有的直方图的边界点可以少于 100。
  
## <a name="density-vector"></a>密度向量  
查询优化器使用密度提高根据相同表或索引视图返回多个列的查询的基数估计。 密度向量针对统计信息对象中的列的每个前缀包含一个密度。 例如，如果统计信息对象包含键列 CustomerId、ItemId、Price，则根据以下每个列前缀计算密度。
  
|列前缀|计算密度所基于的对象|  
|---|---|
|(CustomerId)|具有与 CustomerId 匹配的值的行|  
|(CustomerId, ItemId)|具有与 CustomerId 和 ItemId 匹配的值的行|  
|(CustomerId, ItemId, Price)|具有与 CustomerId、ItemId 和 Price 匹配的值的行|  
  
## <a name="restrictions"></a>限制  
 DBCC SHOW_STATISTICS 不提供空间索引或 xVelocity 内存优化的列存储索引的统计信息。  
  
## <a name="permissions-for-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
若要查看统计信息对象，该用户必须拥有表或用户必须是属于`sysadmin`固定服务器角色、`db_owner`固定数据库角色或`db_ddladmin`固定的数据库角色。
  
SQL Server 2012 SP1 修改了这些权限限制，允许具有 SELECT 权限的用户使用此命令。 请注意，SELECT 权限必须满足以下要求才能运行此命令：
-   用户必须对统计对象中的所有列具有权限  
-   用户必须对筛选条件（如果存在）中的所有列具有权限  
-   表不能具有行级别安全性策略。  
  
若要禁用此行为，请使用跟踪标志 9485。
  
## <a name="permissions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>权限[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC SHOW_STATISTICS 需要针对以下项之一中的成员身份的表的 SELECT 权限：
-   sysadmin 固定服务器角色  
-   db_owner 固定的数据库角色  
-   db_ddladmin 固定的数据库角色  
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>限制和局限为[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC SHOW_STATISTICS 显示控件节点级别上的 Shell 数据库中存储的统计信息。 它不显示是由自动创建的统计信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算节点上。
  
外部表不支持 DBCC SHOW_STATISTICS。
  
## <a name="examples-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>示例：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
### <a name="a-returning-all-statistics-information"></a>A. 返回所有统计信息  
下面的示例显示所有统计信息对于`AK_Address_rowguid`索引`Person.Address`表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。
  
```t-sql
DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);  
GO  
```  
  
### <a name="b-specifying-the-histogram-option"></a>B. 指定 HISTOGRAM 选项  
下面的示例将为 `AK_Address_rowguid`索引显示的统计信息限制为 HISTOGRAM 数据。
  
```t-sql
DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid) WITH HISTOGRAM;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="c-display-the-contents-of-one-statistics-object"></a>C. 显示一个统计信息对象的内容  
 下面的示例显示上 DimCustomer 表 Customer_LastName 统计信息的内容。  
  
```t-sql
-- Uses AdventureWorks  
--First, create a statistics object  
CREATE STATISTICS Customer_LastName   
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName);  
GO  
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName);  
GO  
```  
  
结果显示标头、 密度向量和直方图的一部分。
  
![DBCC SHOW_STATISTICS 结果](../../t-sql/database-console-commands/media/aps-sql-dbccshow-statistics.JPG "DBCC SHOW_STATISTICS 结果")
  
### <a name="d-specifying-the-histogram-option"></a>D. 指定 HISTOGRAM 选项  
这就限制了显示 Customer_LastName 直方图数据的统计信息。
  
```t-sql
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName) WITH HISTOGRAM;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[统计信息](../../relational-databases/statistics/statistics.md)  
[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)  
[删除统计信息 &#40;Transact SQL &#41;](../../t-sql/statements/drop-statistics-transact-sql.md)  
[sp_autostats &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)  
[sp_createstats &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)  
[STATS_DATE &#40;Transact SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
[更新统计信息 (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)  
[sys.dm_db_stats_properties (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
[sys.dm_db_stats_histogram (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
