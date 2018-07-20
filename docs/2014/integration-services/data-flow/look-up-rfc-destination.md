---
title: 查找 RFC 目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eea7cee81892b7ffb5ce35d747c54b413ceb1d62
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252619"
---
# <a name="look-up-rfc-destination"></a>查找 RFC 目标
  使用 **“查找 RFC 目标”** 对话框查找在 SAP Netweaver BW 系统中定义的 RFC 目标。 当可用 RFC 目标列表显示时，选择您需要的目标，然后组件将使用需要的值填充关联的选项。  
  
 SAP BW 源和 SAP BW 目标都使用 **“查找 RFC 目标”** 对话框。 有关这些 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 组件的详细信息，请参阅 [SAP BW 源](sap-bw-source.md) 和 [SAP BW 目标](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 **打开“查找 RFC 目标”对话框**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含 SAP BW 源或目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 SAP BW 源或目标。  
  
3.  在 **“SAP BW 源编辑器”** 或 **SAP BW 目标编辑器”** 中单击 **“连接管理器”** ，以打开编辑器的 **“连接管理器”** 页。  
  
4.  在 **“连接管理器”** 页上的 **“RFC 目标”** 组框中，单击 **“查找”** 显示 **“查找 RFC 目标”** 对话框。  
  
     在“SAP BW 源编辑器”中，仅当“执行模式”为“P - 触发进程链”或“W - 等待通知”时，“RFC 目标”组框才会显示。  
  
## <a name="options"></a>“常规”  
 **目标**  
 查看在 SAP Netweaver BW 系统中定义的 RFC 目标的名称。  
  
 **网关主机**  
 查看网关主机的服务器名称或 IP 地址。 通常，名称或 IP 地址与 SAP 应用程序服务器相同。  
  
 **网关服务**  
 查看网关服务的名称格式`sapgwNN`，其中`NN`是系统编号。  
  
 **程序 ID**  
 查看与 RFC 目标关联的程序 ID。  
  
## <a name="see-also"></a>请参阅  
 [SAP BW 源编辑器&#40;连接管理器页&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 目标编辑器&#40;连接管理器页&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW 的 F1 帮助](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  