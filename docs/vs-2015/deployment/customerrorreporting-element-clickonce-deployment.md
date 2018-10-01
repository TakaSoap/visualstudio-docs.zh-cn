---
title: '&lt;customErrorReporting&gt;元素 （ClickOnce 部署） |Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 422ccaf8e82a2b1813bc876c76a6ff5a7c96f43c
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47478193"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting&gt;元素 （ClickOnce 部署）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[ &lt;customErrorReporting&gt;元素 （ClickOnce 部署）](https://docs.microsoft.com/visualstudio/deployment/customerrorreporting-element-clickonce-deployment)。  
  
指定发生错误时所显示的 URI。  
  
## <a name="syntax"></a>语法  
  
```  
<customErrorReporting  
   uri  
/>  
```  
  
## <a name="remarks"></a>备注  
 此元素为可选元素。 如果没有它，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]显示一个错误对话框，显示异常堆栈。 如果`customErrorReporting`元素存在，则[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]将改为显示由 URI`uri`参数。 目标 URI 将包括外部异常类、 内部异常类和内部异常消息作为参数。  
  
 使用此元素添加到你的应用程序报告功能的错误。 由于生成的 URI 包括有关错误的类型的信息，该信息和显示，例如，相应的故障排除屏幕可以分析你的网站。  
  
## <a name="example"></a>示例  
 以下代码片段演示`customErrorReporting`元素，以及它可能会产生的生成 URI。  
  
```  
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />  
  
Example Generated Error:  
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)


