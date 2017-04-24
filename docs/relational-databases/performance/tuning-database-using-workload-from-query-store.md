---
title: "使用 Query Store 中的工作负荷优化数据库 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f89ed5e87b8fd51e8618a8559679225d91b32de
ms.lasthandoff: 04/11/2017

---
# <a name="tuning-database-using-workload-from-query-store"></a>使用 Query Store 中的工作负荷优化数据库
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


SQL Server 中的 [Query Store](../../relational-databases/performance/how-query-store-collects-data.md) 功能可自动捕获查询、计划和运行时统计信息的历史记录，并将此信息保存在数据库中。 [数据库引擎优化顾问 (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) 支持使用一个新选项来利用 Query Store 自动选择用于优化的适当工作负荷。 对于许多用户而言，使用此功能便不需要显式收集用于优化的工作负荷。 仅当数据库已启用 Query Store 功能时，此功能才可用。 
  
  SQL Server Management Studio **16.4** 或更高版本提供此功能。 
  
<a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>如何在数据库引擎优化顾问 GUI 中优化 Query Store 的工作负荷
---
在 DTA GUI 中的“常规”窗格内选中“Query Store”单选按钮以启用此功能（参阅下图）。
![Query Store 中的 DTA 工作负荷](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
<a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>如何在 dta.exe 命令行实用工具中优化 Query Store 的工作负荷
---
在命令行 (dta.exe) 中，选择 **-iq** 选项来选择 Query Store 中的工作负荷。 

选择 Query Store 中的工作负荷时，可通过命令行调用其他两个选项来帮助优化 DTA 的行为。 无法通过 GUI 调用这些选项：
  1. 要优化的工作负荷事件数：此选项是使用 **-n** 命令行参数指定的，可让用户控制要优化 Query Store 中的多少个事件。 默认情况下，DTA 对此选项使用值 1000。 请注意，DTA 始终根据总持续时间选择开销最大的事件。 
  
  2. 要优化的事件时限：由于 Query Store 包含的查询可能是很久以前执行的，因此，此选项可让用户指定过去的某个时限（以小时为单位），DTA 只考虑优化已执行了该时限的查询。 此选项是使用 **-I** 命令行参数指定的。 

有关详细信息，请参阅 [dta 实用工具](../../tools/dta/dta-utility.md)。

<a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>使用 Query Store 和计划缓存中的工作负荷的差别 
--- 
Query Store 与计划缓存选项之间的差别在于，前者包含已针对数据库执行的、每次重新启动服务器都会保存的查询的更长历史记录， 而计划缓存只包含最近执行的、其计划缓存在内存中的查询的子集。 重新启动服务器时，将会丢弃计划缓存中的项。

<a name="see-also"></a>另请参阅 
--- 
[数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[教程：数据库引擎优化顾问](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)     
[查询存储的数据收集方式](../../relational-databases/performance/how-query-store-collects-data.md)     
[Query Store 最佳做法](../../relational-databases/performance/best-practice-with-the-query-store.md)