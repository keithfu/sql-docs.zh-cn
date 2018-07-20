---
title: 查看表的依赖关系 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- table dependencies [SQL Server]
- dependencies [SQL Server], tables
- displaying dependences
- viewing dependencies
ms.assetid: c4351ef5-e7d0-46e7-8367-88695e9974f8
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34d938ff2df192f80c4474088a63d664b3ebd61d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197147"
---
# <a name="view-the-dependencies-of-a-table"></a>查看表的依赖关系
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看表的依赖关系。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **使用以下工具查看表的依赖关系：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求对数据库具有 VIEW DEFINITION 权限，并对数据库的 sys.sql_expression_dependencies 具有 SELECT 权限。 默认情况下，SELECT 权限仅授予 db_owner 固定数据库角色的成员。 将 SELECT 和 VIEW DEFINITION 权限授予其他用户时，被授权者可以查看数据库中的所有依赖关系。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-dependencies-of-a-table"></a>查看表的依赖关系  
  
1.  在 **“对象资源管理器”** 中，展开 **“数据库”**，再展开其中的某个数据库，然后展开 **“表”**。  
  
2.  右键单击某个表，然后单击“查看依赖关系”。  
  
3.  在“对象依赖关系 \<对象名称>”**对话框中，选择“依赖于 \<对象名称> 的对象”** 或“\<对象名称> 依赖的对象”****。  
  
4.  在 **“依赖关系”** 网格中选择一个对象。 对象类型（如“触发器”或“存储过程”）显示在“类型”框中。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-objects-that-depend-on-a-table"></a>查看依赖于表的对象  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');   
    GO  
  
    ```  
  
#### <a name="to-view-the-objects-on-which-a-table-depends"></a>查看表依赖的对象  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  下面的示例返回依赖于表 `Production.Product`的对象。 将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referenced_id = OBJECT_ID(N'Production.Product');   
    GO  
  
    ```  
  
 有关其他信息，请参阅 [sys.sql_expression_dependencies (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
  