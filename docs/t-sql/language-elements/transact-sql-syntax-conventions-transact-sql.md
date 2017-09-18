---
title: "TRANSACT-SQL 语法约定 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.TSQLExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a1c60d865d1b18eae1cd89ea226e91e8e7b5b9e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>TRANSACT-SQL 语法约定的 Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  下表列出了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 参考的语法关系图中使用的约定，并进行了说明。  
  
|约定|用于|  
|----------------|--------------|  
|大写|[!INCLUDE[tsql](../../includes/tsql-md.md)]关键字。|  
|*斜体*|用户提供的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法的参数。|  
|**粗体**|数据库名、表名、列名、索引名、存储过程、实用工具、数据类型名以及必须按所显示的原样键入的文本。|  
|**下划线**|指示当语句中省略了包含带下划线的值的子句时应用的默认值。|  
||（垂直条）|分隔括号或大括号中的语法项。 只能使用其中一项。|  
|`[ ]`（方括号）|可选语法项。 不要键入方括号。|  
|{}（大括号）|必选语法项。 不要键入大括号。|  
|[**,**...*n*]|指示前面的项可以重复 *n* 次。 各项之间以逗号分隔。|  
|[...*n*]|指示前面的项可以重复 *n* 次。 每一项由空格分隔。|  
|;|[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句终止符。虽然在此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中大部分语句不需要分号，但将来的版本需要分号。|  
|\<标签 >:: =|语法块的名称。 该约定用于对过长语法段或语法单元进行分组和标记，这些语法段或语法单元可在一条语句中的多个位置使用。 可在其中使用语法块的每个位置括在尖括号内的标签指示：\<标签 >。<br /><br /> 一组是集合的表达式，例如\<分组集 >; 列表将集的集合，例如\<复合元素列表 >。|  
  
## <a name="multipart-names"></a>多部分名称  
 除非另外指定，否则，所有对数据库对象名的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 引用将是由四部分组成的名称，格式如下：  
  
 *server_name* **。**[*database_name*]**。**[*schema_name*]**。***object_name*  
  
 | *database_name***。**[*schema_name*]**。***object_name*  
  
 | *schema_name***。***object_name*  
  
 *|object_name*  
  
 *server_name*  
 指定链接的服务器名称或远程服务器名称。  
  
 *database_name*  
 如果对象驻留在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中，则指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的名称。 在链接服务器中，对象时*database_name*指定 OLE DB 目录。  
  
 *schema_name*  
 如果对象在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，则指定包含对象的架构的名称。 在链接服务器中，对象时*schema_name*指定 OLE DB 架构名称。  
  
 *object_name*  
 对象的名称。  
  
 引用某个特定对象时，不必总是指定服务器、数据库和架构供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]标识该对象。 但是，如果找不到对象，则返回错误。  
  
> [!NOTE]  
>  为了避免名称解析错误，建议只要指定了架构范围内的对象时就指定架构名称。  
  
 若要省略中间节点，请使用句点来指示这些位置。 下表显示了对象名的有效格式。  
  
|对象引用格式|Description|  
|-----------------------------|-----------------|  
|*服务器* **。** *数据库* **。** *架构* **。** *对象*|四个部分的名称。|  
|*服务器* **。** *数据库* **...** *对象*|省略架构名称。|  
|*服务器* **...** *架构* **。** *对象*|省略数据库名称。|  
|*服务器* **...** *对象*|省略数据库和架构名称。|  
|*数据库* **。** *架构* **。** *对象*|省略服务器名。|  
|*数据库* **...** *对象*|省略服务器和架构名称。|  
|*架构* **。** *对象*|省略服务器和数据库名称。|  
|*对象*|省略服务器、数据库和架构名称。|  
  
## <a name="code-example-conventions"></a>代码示例约定  
 除非专门说明，否则，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 参考中提供的示例都已使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 及其以下选项的默认设置进行了测试：  
  
-   ANSI_NULLS  
  
-   ANSI_NULL_DFLT_ON  
  
-   ANSI_PADDING  
  
-   ANSI_WARNINGS  
  
-   CONCAT_NULL_YIELDS_NULL  
  
-   QUOTED_IDENTIFIER  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 参考中的大多数代码示例都已在运行区分大小写排序顺序的服务器上进行了测试。 测试服务器通常运行 ANSI/ISO 1252 代码页。  
  
 许多代码示例前缀以字母的 Unicode 字符的字符串常量**N**。而无需**N**前缀，该字符串转换为数据库的默认代码页。 此默认代码页可能不识别某些字符。  
  
## <a name="applies-to-references"></a>“适用于”引用  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]参考包括与相关的主题[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，和[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]。 每个主题的顶部附近是一个指示哪个产品支持本主题要点的部分。 如果省略了某一产品，则主题所述功能在此产品中不可用。 例如，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中介绍了可用性组。 **CREATE AVAILABILTY GROUP**主题指出它适用于**SQL Server (SQL Server 2012 至当前版本)**因为它不适用于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，或[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 在某些情况下，主题的常规要点可用于某一产品，但所有参数不受支持。 例如，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中介绍了包含的数据库用户。 **CREATE USER**语句可在任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品，但是**WITH PASSWORD**语法不能与旧版结合使用。 在此情况下，将其他 **适用于** 部分插入到该主题正文中相应的参数说明中。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)  
  
  


