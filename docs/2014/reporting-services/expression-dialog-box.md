---
title: 表达式对话框 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
- sql12.rtp.rptdesigner.expression.f1
helpviewer_keywords:
- Expression dialog box [Reporting Services]
ms.assetid: e6c74ccb-4594-4d4f-b958-618d710e34eb
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2b2ec18b03081d3469e9187db6043ba27406389b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207673"
---
# <a name="expression-dialog-box"></a>“表达式”对话框
  使用**表达式**对话框可以编写[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]表达式的报表项属性。 您可以使用表达式来设置多个属性，包括颜色、字体和边框。 在运行时，报表处理器对表达式进行计算，然后用结果替代属性的值。  
  
 表达式可能很简单，也可能很复杂。 可以直接在设计图面上的文本框或对话框中键入简单表达式。 若要创建复杂表达式，请使用**表达式**对话框。 一次只能创建一个表达式。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)。  
  
 若要打开“表达式”对话框，请单击对话框中的表达式 (**fx**) 按钮，或者从“属性”窗格的快捷菜单或下拉列表中选择“表达式”。 有关详细信息，请参阅[表达式在报表中使用&#40;报表生成器和 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)。  
  
 **“表达式”** 对话框包含代码窗口、类别树、类别项、说明窗格和示例窗格。  
  
 “表达式”对话框是上下文相关的；根据你所使用的表达式类别，各类别项和说明也会相应地变化。 表达式对话框支持 IntelliSense、语句完成、函数调用示例和语法着色功能，从而便于您检测语法错误。  
  
## <a name="expression-constructs"></a>表达式构造  
 表达式以等号 (=) 开头，可以包含常量、文字、运算符以及对内置字段、内置集合、内置函数、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 运行库函数、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 公共语言运行时类和自定义函数的引用。 以下列表介绍了可添加到表达式中的类别和值。  
  
 **设置表达式：***\<属性名称 >*   
 要为其定义表达式的属性的名称。 此外，还可以在“属性”窗格中按名称设置此属性。  
  
 **常量**  
 为基于常量的属性提供了对该属性有效的预定义值列表。 例如，基于颜色的属性会显示有效的颜色名称。 对于布尔数据类型的属性，值为`True`和`False`。  
  
 并不是所有支持表达式的项都可设置为常量。 如果某属性不能设置为常量值，说明窗格将会提供此信息。  
  
 **内置字段**  
 提供的列表包含可以在表达式中使用的全局集合中的项。 某些集合只有在报表发布到服务器后才受支持。 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
 **Parameters**  
 提供报表参数的列表。  
  
 **字段 (** *\<所选数据集 >* **)**  
 显示在数据集类别中选择的数据集的字段列表。 双击某字段可将该字段复制到“表达式”框。  
  
 **数据集**  
 提供可用数据集的列表并显示数据集的成员字段。  
  
 **变量**  
 显示报表变量的列表。 有关详细信息，请参阅[报表和组变量集合引用（报表生成器和 SSRS）](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)。  
  
 **运算符**  
 显示可包含在计算或字符串操作中的运算符。 有关详细信息，请参阅[表达式中的运算符（报表生成器和 SSRS）](report-design/operators-in-expressions-report-builder-and-ssrs.md)。  
  
 **常见函数**  
 显示按类型分组后的常见函数。 当您在“项”窗格中选择函数时，相应的说明和示例会显示出来。  
  
 常见函数包括内置报表函数和聚合函数[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]运行时库函数，并[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]公共语言运行时 (CLR) 类中的<xref:System.Math>和<xref:System.Convert>命名空间。 你还可以添加对没有显示在类别列表中的 CLR 类和外部程序集的引用。 有关详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
## <a name="options"></a>选项  
 代码窗口  
 使用顶部窗格中的代码窗口可以键入表达式。 在打开 **“表达式”** 对话框时，代码窗口将包含该表达式。 您可替换或修改该表达式。 您可以添加函数调用、运算符、常量、字段、参数、全局集合中的项以及对自定义代码的引用。 在您进行更改时，代码窗口会显示您所做的更改。  
  
 红色波浪下划线指示语法错误。 将光标悬停在带有下划线的文本上查看错误消息。  
  
 当键入跟有标点分隔符的全局集合字词时，您将看到可用成员或属性的下拉列表。 在下拉列表中，可以键入前几个字符以及制表符来自动填充选项。  
  
 当键入跟有左括号的函数名时，您将看到一个提供关于参数和函数返回值信息的工具提示。  
  
 **类别**  
 显示表达式的不同类别。 选择一个类别将建立用于创建表达式的上下文，并更改“项”窗格中的有效值列表。 例如，对于一个用于文本框值表达式，展开常见函数，然后选择要显示的聚合函数`Avg`， `Count`，和中的其他函数**项**窗格。  
  
 **项**  
 显示所选类别的有效值列表。 双击一个项可以将此项的表达式文本添加到代码窗口中的插入点处。  
  
 **值**  
 根据所选的类别和项，第三个窗格将包含说明、示例表达式或有效值列表。 拖动该对话框的边缘可以加宽示例区域。  
  
## <a name="see-also"></a>请参阅  
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [设置数字和日期格式&#40;报表生成器和 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [参数集合引用（报表生成器和 SSRS）](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [组表达式示例（报表生成器和 SSRS）](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [筛选器公式示例&#40;报表生成器和 SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [表达式中的内置集合&#40;报表生成器和 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)   
 [添加表达式（报表生成器和 SSRS）](report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
