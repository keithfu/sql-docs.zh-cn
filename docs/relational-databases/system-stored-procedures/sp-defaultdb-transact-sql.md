---
title: "sp_defaultdb (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_defaultdb_TSQL
- sp_defaultdb
dev_langs: TSQL
helpviewer_keywords: sp_defaultdb
ms.assetid: 663b859f-c6da-4942-95a6-60b93d05654e
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 277d4e4f714e4f95ecd80f0a770ef7d8f820e3d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdefaultdb-transact-sql"></a>sp_defaultdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改的默认数据库[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)相反。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_defaultdb [ @loginame = ] 'login', [ @defdb = ] 'database'   
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame=**] *登录*  
 登录名。 *登录名*是**sysname**，无默认值。 *登录名*可以是现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录或 Windows 用户或组。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不存在 Windows 用户或用户组的登录名，则会自动添加该登录名。  
  
 [  **@defdb=**] *数据库*  
 新的默认数据库的名称。 *数据库*是**sysname**，无默认值。 *数据库*必须已存在。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_defaultdb**调用 ALTER LOGIN。 此语句支持附加选项。 有关更改默认数据库的信息，请参阅[ALTER LOGIN &#40;Transact SQL &#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_defaultdb**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
 以下示例将 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `Victoria` 的默认数据库。  
  
```  
EXEC sp_defaultdb 'Victoria', 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantdbaccess (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  