---
title: IDebugStackFrame2::EnumProperties |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5cbbdfe2585ec7fa90b2e98bbd76baa5093f296e
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47468805"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

本主题的最新版本，请参阅[IDebugStackFrame2::EnumProperties](https://docs.microsoft.com/visualstudio/extensibility/debugger/reference/idebugstackframe2-enumproperties)。  
  
创建与该堆栈帧，如本地变量关联的属性的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumProperties (   
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,  
   UINT                      nRadix,  
   REFIID                    refiid,  
   DWORD                     dwTimeout,  
   ULONG*                    pcelt,  
   IEnumDebugPropertyInfo2** ppEnum  
);  
```  
  
```csharp  
int EnumProperties (   
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,  
   uint                        nRadix,  
   ref Guid                    refiid,  
   uint                        dwTimeout,  
   out uint                    pcelt,  
   out IEnumDebugPropertyInfo2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFieldSpec`  
 [in]中的标志的组合[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举，用于指定哪些字段中枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构是必填。  
  
 `nRadix`  
 [in]用于格式化数值的任何信息的基数。  
  
 `refiid`  
 [in]筛选器用于选择其中一个 GUID [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构是否进行枚举，如`guidFilterLocals`。  
  
 `dwTimeout`  
 [in]最大时间 （毫秒），此方法返回前等待。 使用`INFINITE`无限期等待。  
  
 `pcelt`  
 [out]返回枚举的属性的数目。 这是调用相同[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)方法。  
  
 `ppEnum`  
 [out]返回[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，其中包含所需属性的列表。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法允许一次调用检索所有所选的属性，因为它是比按顺序调用更快[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)并[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)   
 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)   
 [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)   
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
