---
title: 更新行集中的数据 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34071ebd4c0f4a365d654eb858ea419383ceeaa6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425696"
---
# <a name="updating-data-in-rowsets"></a>更新行集中的数据
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据使用者更新可修改的行中包含的数据集时。 使用者请求支持时，创建一个可修改的行集**IRowsetChange**或**IRowsetUpdate**接口。  
  
 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序可修改行集均使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持行集。 行集属性 DBPROP_LOCKMODE 更改游标中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并发控制行为，并确定在可更新行集中提取行集的行和生成数据完整性错误的行为。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持在更新前后同步行。  
  
> [!NOTE]  
>  可使用 IRowChange::SetColumns 设置行对象的一个或多个指定列的值。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [更新 SQL Server 游标中的数据](updating-data-in-sql-server-cursors.md)  
  
-   [重新同步行](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  