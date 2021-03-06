---
title: 选择源表和视图（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f99b94c133ba2a8bfd8bbe6d7b78bd455061409
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050129"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>选择源表和源视图（SQL Server 导入和导出向导）
  使用**选择源表和视图**页后，可以指定的表和视图以从数据源复制到目标。  
  
> [!NOTE]  
>  如果选中了“表复制”选项，则不必复制表中的所有列。 选择目标表后, 单击编辑映射以显示**列映射**对话框。 选择**\<忽略 >** 中**目标**列**列映射**你想要跳过的列对话框。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关用于启动向导，选项以及已成功运行该向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
  
### <a name="tables-and-views-list"></a>表和视图列表  
 **数据源**  
 使用这些复选框，可以从可用表和视图的列表中进行选择，以复制到目标。 如果选择了源表或源视图并且不执行其他操作，将从源不加更改地复制架构和数据。  
  
 **目标**  
 从列表中为每个源表选择一个目标表。  
  
> [!NOTE]  
>  如果此时在向导中创建目标表中的暂停[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]或另一种工具，新表不是立即出现在可用目标表的列表。 若要刷新目标表的列表，请倒退两页回到**选择目标**页上，重新选择目标数据库，然后再次前进到**选择源表和视图**。  
  
### <a name="other-options"></a>其他选项  
 **编辑映射**  
 使用**列映射**对话框中，指定要接收源数据的目标列。 可以通过选择复制列的子集\<忽略 > 中**目标**的列**列映射**你想要跳过的列对话框。  
  
 **预览**  
 预览中的源数据**预览数据**对话框验证之前执行导入或导出。 **预览数据**对话框显示最多 200 行数据。  
  
 预览数据后，可能需要更改为数据源和目标选定的选项。 若要进行这些更改，请在 **“选择源表和源视图”** 页，单击 **“后退”** 返回到可以更改选项的上一页。  
  
  
