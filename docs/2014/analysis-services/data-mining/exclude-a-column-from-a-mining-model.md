---
title: 从挖掘模型中排除列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 656e9dc84c2556cc4f5ea76858764ee9c1fbf556
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068873"
---
# <a name="exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列
  在创建新的挖掘模型时，您可能不希望使用模型基于的挖掘结构中存在的所有列。 例如，您可能添加了一个客户名称列来用于钻取，但不想将该列用于建模。 或者，您可能决定为一个列创建具有不同离散化的多个副本，并且在每个模型中仅使用这些副本中的一个，而忽略其余副本。 您还可以有选择地在若干不同模型中添加输入列，看看所添加的变量是如何影响输出列的。  
  
 您不需要为每个列组合都创建新的挖掘结构；相反，您只需将某个列标记为不在特定的模型中使用。  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列  
  
1.  在 **中的数据挖掘设计器的** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，在有关的挖掘模型下，选择与要排除的列相对应的单元。  
  
2.  从下拉列表框中选择“忽略”。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)  
  
  
