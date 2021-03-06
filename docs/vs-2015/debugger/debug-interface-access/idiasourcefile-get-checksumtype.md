---
title: IDiaSourceFile::get_checksumType | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f859bce63e2976b23ab613e249dad41b2bc63486
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190702"
---
# <a name="idiasourcefilegetchecksumtype"></a>IDiaSourceFile::get_checksumType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索的校验和类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_checksumType (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回校验和类型。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 校验和类型是可以映射到校验和算法的值。 例如，在标准的 PDB 文件格式可以通常具有下列值之一：  
  
|校验和类型|CryptoAPI 标签|描述|  
|-------------------|---------------------|-----------------|  
|0|\<none>|不存在的校验和。|  
|1|`CALG_MD5`|使用 MD5 哈希算法生成的校验和。|  
|2|`CALG_SHA1`|使用 SHA1 哈希算法生成的校验和。|  
  
 `CryptoAPI`标签是从`ALG_ID`枚举。 哈希算法的详细信息，请查阅`CryptoAPI`部分中的 Microsoft [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)]。  
  
 若要获取的源文件的实际校验和字节，请调用[idiasourcefile:: Get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)
