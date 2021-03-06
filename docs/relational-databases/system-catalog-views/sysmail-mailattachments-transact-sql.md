---
title: sysmail_mailattachments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c263f7e3df69b6eb3d9517b2dc973a1cb4102f7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627305"
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提交到数据库邮件的每个附件都在视图中占一行。 如果需要有关数据库附件的信息，则请使用该视图。 若要查看通过数据库邮件使用处理的所有电子邮件[sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|附件的标识符。|  
|**mailitem_id**|**int**|包含附件的邮件项的标识符。|  
|**filename**|**nvarchar(520)**|附件的文件名。 当**attach_query_result**为 1 并**query_attachment_filename**为 NULL，数据库邮件会创建任意文件名。|  
|**filesize**|**int**|附件的大小（字节）。|  
|**附件**|**varbinary(max)**|附件的内容。|  
|**last_mod_date**|**datetime**|上次修改行的日期和时间。|  
|**last_mod_user**|**sysname**|上次修改行的用户。|  
  
## <a name="remarks"></a>备注  
 排除数据库邮件故障时，请使用该视图来查看附件的属性。  
  
 附件存储在系统表中可能会导致**msdb**数据库增长。 使用**sysmail_delete_mailitems_sp**若要删除邮件项及其关联的附件。 有关详细信息，请参阅[创建 SQL Server 代理作业以存档数据库邮件和事件日志](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)。  
  
## <a name="permissions"></a>Permissions  
 授予**sysadmin**固定的服务器角色和**DatabaseMailUserRole**数据库角色。 成员执行时**sysadmin**固定服务器角色，此视图显示所有附件。 所有其他用户仅可查看他们已提交的消息的附件。  
  
## <a name="see-also"></a>请参阅  
 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
