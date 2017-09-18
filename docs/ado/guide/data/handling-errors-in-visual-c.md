---
title: "在 Visual c + + 中处理错误 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72aeaf6c2b31f6f7933bd64065ab57e23ef7e92b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="handling-errors-in-visual-c"></a>在 Visual c + + 中处理错误
在 COM 中，大多数操作返回一个 HRESULT 返回代码指示函数是否已成功完成。 #Import 指令生成每个"原始"方法或属性周围的包装代码，并检查返回的 HRESULT。 如果 HRESULT 指示失败，包装代码会引发 COM 错误通过，HRESULT 返回代码的调用 _com_issue_errorex() 作为自变量中。 COM 错误对象可捕获在**try catch**块。 （为效率的起见，捕获 _com_error 对象的引用。）  
  
 请记住，这些是 ADO 错误： 它们来自 ADO 操作失败。 基础提供程序返回的错误显示为**错误**中的对象**连接**对象的**错误**集合。  
  
 #Import 指令仅创建方法和属性在 ADO.dll 中声明的错误处理例程。 但是，你可以利用此相同的错误处理机制通过编写自己的错误检查宏或内联函数。 请参阅示例的主题 Visual C++® 扩展。