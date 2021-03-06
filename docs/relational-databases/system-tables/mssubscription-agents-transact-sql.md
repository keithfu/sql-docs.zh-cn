---
title: MSsubscription_agents (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4be8f754dce7863575721996a9a039b7a3686e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670115"
---
# <a name="mssubscriptionagents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_agents**表由分发代理和可更新订阅的触发器来跟踪订阅属性。 此表存储在订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|行的 ID。|  
|**publisher**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**subscription_type**|**int**|订阅类型：<br /><br /> 0 = 推送。<br /><br /> 1 = 请求<br /><br /> 2 = 匿名请求。|  
|**queue_id**|**sysname**|ID[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列在发布服务器。 *queue_id*设置为**SQL**的基于 SQL 的排队更新。|  
|**update_mode**|**tinyint**|更新的类型：<br /><br /> **0** = 只读的。<br /><br /> **1** = 立即更新。<br /><br /> **2** = 使用消息队列的排队更新。<br /><br /> **3** = 立即更新，以排队更新作为故障转移使用消息队列。<br /><br /> **4** = 使用 SQL Server 队列的排队更新。<br /><br /> **5** = 立即更新排队的更新作为故障转移，使用 SQL Server 队列。|  
|**failover_mode**|**bit**|如果选择了更新的故障转移类型，则此参数值为选择的故障转移类型：<br /><br /> **0** = 立即更新正在使用。 不启用故障转移。<br /><br /> **1** = 排队更新正在使用。 已启用故障转移。 中指定要用于故障转移的队列*update_mode*值。|  
|**spid**|**int**|当前正在运行或刚运行过的分发代理使用的连接的系统进程 ID。|  
|**login_time**|**datetime**|当前正在运行或刚运行过的分发代理连接的日期和时间。|  
|**allow_subscription_copy**|**bit**|指定是否允许使用复制订阅数据库的功能。|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|代表附加订阅版本的唯一标识符。|  
|**last_sync_status**|**int**|当前正在运行或刚运行过的分发代理的最后运行状态。 状态可以为：<br /><br /> **1** = 启动。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**last_sync_summary**|**sysname**|当前正在运行或刚运行过的分发代理的上一条消息。 状态可以为：<br /><br /> **已启动。**<br /><br /> **已成功。**<br /><br /> **正在进行。**<br /><br /> **空闲。**<br /><br /> **重试。**<br /><br /> **失败。**|  
|**last_sync_time**|**datetime**|日期和时间*last_sync_summary*并*last_sync_status*列已更新。 作为 SqlServer 代理服务作业运行的请求分发代理或匿名分发代理不更新这些列。 在这种情况下，会将历史记录信息记录到作业历史表中。|  
|**queue_server**|**sysname**|仅限内部使用。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
