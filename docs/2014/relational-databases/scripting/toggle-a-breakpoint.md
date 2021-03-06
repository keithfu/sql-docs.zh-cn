---
title: 切换断点 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b6060a38e6cfa5fa826ac255d05a1f5e72018e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064857"
---
# <a name="toggle-a-breakpoint"></a>切换断点
  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句上设置断点的操作称为切换断点。  
  
## <a name="breakpoints"></a>断点  
 设置断点后，语句左侧的灰色栏中会出现一个图标来表示该断点。 该图标称为断点符号。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 断点适用于整个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 打开断点时，调试器会突出显示相关联的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
 如果一行中存在多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，可以为每个语句切换一个断点。 单击窗口左侧的灰色栏可以在行中的第一个语句上切换断点。 您可以通过以下方法在后续语句中切换断点：突出显示该语句的任何部分，或将光标移动到该语句中，然后按 F9 或单击 **“调试”** 菜单上的 **“切换断点”** 。 如果一行中有多个断点，则只有一个断点符号位于左侧的灰色栏中。  
  
 在切换某一断点后，您可以对该断点执行不同的操作，例如编辑其属性或临时禁用该断点。 有关详细信息，请参阅 [Transact-SQL 断点](transact-sql-breakpoints.md)。  
  
## <a name="toggle-a-breakpoint"></a>切换断点  
 **切换 Transact-SQL 语句上的断点**  
  
1.  单击 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句左侧的灰色栏。  
  
2.  或者，突出显示语句的任何部分，或将光标移到语句上，然后执行下列两个操作之一：  
  
    -   按 F9。  
  
    -   在 **“调试”** 菜单上，单击 **“切换断点”**。  
  
  
