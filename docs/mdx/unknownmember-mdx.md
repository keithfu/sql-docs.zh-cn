---
title: "UnknownMember (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UnknownMember
dev_langs:
- kbMDX
helpviewer_keywords:
- UnknownMember function
ms.assetid: 5ae39cbe-65c8-4a59-9548-71b28ecf6eb5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 131993b1038229138df3e7d084b5d842693b7f0f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回与级别或成员相关联的未知成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]创建的未知的成员，以将事实数据表数据关联的层次结构，不知道层次结构时。 未知成员可位于下列级别之一：  
  
-   位于未聚合的属性层次结构的顶级。  
  
-   在下面的第一个级别**所有**自然层次结构级别。  
  
-   位于非自然层次结构的任何一级。  
  
 如果指定一个成员表达式，则**UnknownMember**函数将返回指定成员的未知的成员子级。 如果指定的成员不存在，该函数将返回空。  
  
 如果指定一个层次结构表达式，则**UnknownMember**如果存在，函数将返回最高级别未知的成员。  
  
 如果上级别或成员，不存在未知的成员**UnknownMember**函数创建 null 的成员。  
  
> [!NOTE]  
>  如果层次结构或成员中不存在未知成员，将生成一个错误。  
  
## <a name="examples"></a>示例  
 下面的示例为 Measures 维度的所有成员返回 Product 属性层次结构中 All Products 成员的未知成员。  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 下面的示例为 Measures 维度的所有成员返回 Product Categories 层次结构的未知成员。  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
