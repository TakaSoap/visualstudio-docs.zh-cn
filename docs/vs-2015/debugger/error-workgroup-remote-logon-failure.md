---
title: 错误：工作组远程登录失败 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.workgroup_remote_logon_failure
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- logon failure, remote debugging
- remote debugging, logon failure
ms.assetid: 7be2c5bb-40fe-48d6-8cfc-c231fbd3d64e
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 09f018982b81535ae23eafe7158aa88c0b6b08a7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438338"
---
# <a name="error-workgroup-remote-logon-failure"></a>错误：工作组远程登录失败
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此错误显示如下：  
  
 登录失败: 未知的用户名或密码不正确  
  
 **原因**  
  
 当在工作组上的计算机进行调试，并尝试连接到远程计算机时可能发生此错误。 可能的原因包括：  
  
- 远程计算机上没有匹配用户名和密码的帐户。  
  
- 如果 Visual Studio 计算机和远程计算机都在工作组上，远程计算机的默认**本地安全策略**设置可能导致此错误。 **本地安全策略**默认设置为**仅来宾-本地用户以来宾身份验证**。 要在此设置上调试，必须在远程计算机上将设置更改为**经典-本地用户以自己的身份验证**。   
  
> [!NOTE]
> 你必须是管理员才能执行以下任务。  
  
### <a name="to-open-the-local-security-policy-window"></a>打开“本地安全策略”窗口  
  
1. 启动 **secpol.msc** Microsoft 管理控制台管理单元。 在 Windows 搜索、Windows“运行”框中或命令提示符处键入 secpol.msc。   
  
### <a name="to-add-user-rights-assignments"></a>添加用户权限分配  
  
1. 打开 Loca  
  
2. 打开“本地安全策略”窗口。  
  
3. 展开“本地策略”文件夹。  
  
4. 单击“用户权限分配”。  
  
5. 在**策略**列中，双击**调试程序**，以在**本地安全策略设置**对话框中查看当前本地组策略分配。  
  
     ![本地安全策略的用户权限](../debugger/media/dbg-err-localsecuritypolicy-userrightsdebugprograms.png "DBG_ERR_LocalSecurityPolicy_UserRightsDebugPrograms")  
  
6. 若要添加新用户，请单击“添加用户或组”按钮。  
  
### <a name="to-change-the-sharing-and-security-model"></a>更改“共享和安全模型”  
  
1. 打开“本地安全策略”窗口。  
  
2. 展开“本地策略”文件夹。  
  
3. 单击“安全选项”。  
  
4. 在中**策略**列中，双击**网络访问：本地帐户的共享和安全模型**。  
  
5. 在**网络访问：本地帐户的共享和安全模型**对话框框中，将值更改为**经典-本地用户以自己的身份验证**然后单击**应用**按钮。  
  
     ![本地安全策略安全选项](../debugger/media/dbg-err-localsecuritypolicy-securityoptions-networkaccess.png "DBG_ERR_LocalSecurityPolicy_SecurityOptions_NetworkAccess")  
  
## <a name="see-also"></a>请参阅  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [远程调试](../debugger/remote-debugging.md)
