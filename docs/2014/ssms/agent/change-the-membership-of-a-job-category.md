---
title: 更改作业类别的成员身份 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f956a6f87142a9b9bae2d8398d69e3fd3ae08c9c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106167"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
  本主题介绍如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理对象更改作业类别的成员身份。  
  
 作业类别有助于您组织作业，从而更容易筛选和分组。 可以创建自己的作业类别。 还可以更改作业类别中的 Microsoft SQL Server 代理作业成员身份。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要更改作业类别的成员身份，请使用**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>更改作业类别的成员身份  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开您想要在其中编辑作业类别的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  右键单击 **“作业”** 文件夹，然后选择 **“管理作业类别”**。  
  
4.  在“管理作业类别server_name” 对话框中，选择要编辑的作业类别，然后单击“查看作业”。  
  
5.  选中 **“显示所有作业”** 复选框。  
  
6.  若要向类别中添加作业，请在主网格中选中与作业对应的 **“选择”** 列中的复选框。 若要从类别中删除作业，请清除该框。 完成后，单击 **“确定”**。  
  
7.  关闭“管理作业类别server_name” 对话框。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>更改作业类别的成员身份  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_update_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **更改作业类别的成员身份**  
  
 使用`JobCategory`类通过使用一种编程语言的选择，如 Visual Basic、 Visual C# 或 PowerShell。  
  
  
