---
title: 发行说明（适用于 SQL Server 的 OLE DB 驱动程序） | Microsoft Docs
ms.date: 07/03/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 01ea0242637f4dd5c813808b3b840d3a5a86df9a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789115"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 Microsoft OLE DB 驱动程序发行说明
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

本页介绍 Microsoft OLE DB 驱动程序的每个版本中添加适用于 SQL Server。

## <a name="whats-new-in-version-1810"></a>版本 18.1.0 中的新增功能

**添加的功能：**

* 为支持`UseFMTONLY`连接字符串关键字和`SSPROP_INIT_USEFMTONLY`初始化属性。
`UseFMTONLY` 控制元数据的检索方式连接到时[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本。  
有关详细信息，请参阅：
  * [将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**修复的 bug:**

* 修改后的 BCP 格式文件的正确版本。 OLE DB 驱动程序 18.0 错误地将 BCP 格式文件的版本设置为 18.0 而不是 11.0。 不能通过 OLE DB 驱动程序 18.1 读取生成的 OLE DB 驱动程序 18.0 的格式文件。 如果您需要使用生成的驱动程序和新的驱动程序的以前版本的格式文件，可以手动编辑文件以将版本更改为 11.0。

## <a name="whats-new-in-version-1802"></a>版本 18.0.2 中的新增功能

**添加功能**:

* 为支持`MultiSubnetFailover`连接字符串关键字和`SSPROP_INIT_MULTISUBNETFAILOVER`初始化属性。  
有关详细信息，请参阅：  
  * [适用于 SQL Server 的 OLE DB 驱动程序对高可用性和灾难恢复的支持](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>另请参阅
[适用于 SQL Server 的 Microsoft OLE DB 驱动程序](oledb-driver-for-sql-server.md)
