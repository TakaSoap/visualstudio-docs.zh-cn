---
title: “程序集信息”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vb.ProjectPropertiesAssemblyInfo
helpviewer_keywords:
- Assembly Information dialog box
ms.assetid: 8f1f6449-e03d-4a5b-9076-d3b1f84ada48
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1a6af96afbba5e60d950947470f98e2c633caf24
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47479260"
---
# <a name="assembly-information-dialog-box"></a>“程序集信息”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题的最新版本，请参阅[程序集信息对话框](https://docs.microsoft.com/visualstudio/ide/reference/assembly-information-dialog-box)。  
  
  
“程序集信息”对话框用于指定 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 全局程序集特性的值，这些特性存储为你的项目自动创建的 AssemblyInfo 文件中。 在“解决方案资源管理器”中，对于 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]，此文件位于“我的项目”节点中（单击“显示所有文件”可以查看它）；对于 **，此文件位于“属性”**[!INCLUDE[csprcs](../../includes/csprcs-md.md)]下。 有关程序集特性的详细信息，请参阅[特性](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)。  
  
 若要访问此对话框，请在“解决方案资源管理器”中选择项目节点，然后在“项目”菜单上单击“属性”。 当“项目设计器”出现时，单击“应用程序”选项卡。在“应用程序”页上，单击“程序集信息”按钮。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **标题**  
 指定程序集清单的标题。 对应到 <xref:System.Reflection.AssemblyTitleAttribute>。  
  
 **说明**  
 指定程序集清单的可选描述。 对应到 <xref:System.Reflection.AssemblyDescriptionAttribute>。  
  
 **公司**  
 指定程序集清单的公司名称。 对应到 <xref:System.Reflection.AssemblyCompanyAttribute>。  
  
 **产品**  
 指定程序集清单的产品名称。 对应到 <xref:System.Reflection.AssemblyProductAttribute>。  
  
 **版权信息**  
 指定程序集清单的版权声明。 对应到 <xref:System.Reflection.AssemblyCopyrightAttribute>。  
  
 **商标**  
 指定程序集清单的商标。 对应到 <xref:System.Reflection.AssemblyTrademarkAttribute>。  
  
 **程序集版本**  
 指定程序集的版本。 对应到 <xref:System.Reflection.AssemblyVersionAttribute>。  
  
 **文件版本**  
 指定版本号，该版本号指示编译器使用 Win32 文件版本资源的特定版本。 对应到 <xref:System.Reflection.AssemblyFileVersionAttribute>。  
  
 **GUID**  
 标识程序集的唯一 GUID。 创建项目时，Visual Studio 会生成程序集的 GUID。 对应到 <xref:System.Guid>。  
  
 **非特定语言**  
 指定程序集支持的区域性。 对应到 <xref:System.Resources.NeutralResourcesLanguageAttribute>。 默认值为“(无)”。  
  
 **使程序集 COM 可见**  
 指定程序集中的类型是否可由 COM 使用。 对应到 <xref:System.Runtime.InteropServices.ComVisibleAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [应用程序页、项目设计器 (Visual Basic)](../../ide/reference/application-page-project-designer-visual-basic.md)   
 [特性](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)


