---
title: "部署自定义程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
caps.latest.revision: 46
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bae986bea4e252d15bce495892e60c2a7e7d6064
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-custom-assembly"></a>部署自定义程序集
  若要部署中的自定义程序集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，将程序集放在应用程序文件夹中的报表设计器和报表服务器。 默认情况下，自定义程序集被授予**执行**中的权限[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 若要授予自定义程序集之外的 Execute 权限的权限，你将需要编辑报表服务器的 rssrvpolicy.config 配置文件和报表设计器预览窗口的 rspreviewpolicy.config 配置文件。 也可以选择将自定义程序集安装到全局程序集缓存 (GAC) 中。  
  
> [!NOTE]  
>  有两个报表设计器预览模式: 预览选项卡和弹出预览窗口启动报表项目时启动**DebugLocal**模式。 预览选项卡执行使用的所有报表表达式**FullTrust**权限设置，而不适用于安全策略设置。 弹出式预览窗口旨在模拟报表服务器的功能，因此具有策略配置文件，您或管理员必须修改该文件才能在报表设计器中使用自定义程序集。 此弹出式预览还锁定自定义程序集。 因此，您需要关闭预览窗口，才能修改或更新自定义程序集代码。  
  
###### <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>在 Reporting Services 中部署自定义程序集  
  
1.  将自定义程序集从生成位置复制到报表服务器的 bin 文件夹或报表设计器文件夹中。 报表服务器的 bin 文件夹的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin。 报表设计器的默认位置为 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
     通过将自定义程序集放入报表服务器 bin 文件夹中，您可以发布引用自定义程序集的报表；而通过将其放在报表设计器文件夹中，您可以在报表设计器中运行和调试引用自定义程序集的报表。  
  
     如果您需要向自定义程序集代码授予超过默认执行权限的权限，请执行以下操作：  
  
2.  打开相应的配置文件。 rssrvpolicy.config 的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer。 rspreviewpolicy.config 的默认位置为 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
3.  为自定义程序集添加代码组。 有关详细信息，请参阅[安全开发 &#40;Reporting Services &#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="updating-custom-assemblies"></a>更新自定义程序集  
 有时，您可能需要更新当前正在由多个已发布报表引用的自定义程序集的版本。 如果该程序集已位于报表服务器的 bin 目录或报表服务器中，并且程序集的版本号以某种方式递增或更改，则当前发布的报表将不再正常工作。 你将需要更新中引用的程序集版本**CodeModules**报表定义的元素，然后重新发布报表。 如果您知道您将频繁地更新自定义程序集，并且您当前发布的报表需要引用新程序集，则您可能需要考虑在特定程序集的所有更新中使用同一个版本号。  
  
 如果您不需要当前发布的报表引用程序集的新版本，则可以将自定义程序集部署到全局程序集缓存。 全局程序集缓存可以保持同一个程序集的多个版本，这样，您当前的报表可以引用程序集的前一个版本，而新发布的报表可以引用更新后的程序集。 此外，另一个方法是设置报表服务器的绑定重定向，以强制将旧程序集的所有请求重定向到新程序集。 您需要修改报表服务器 Web.config 文件和报表服务器 ReportService.exe.config 文件。 该条目可能如下所示：  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [使用程序集和全局程序集缓存](http://go.microsoft.com/fwlink/?LinkId=63912)  
  
  