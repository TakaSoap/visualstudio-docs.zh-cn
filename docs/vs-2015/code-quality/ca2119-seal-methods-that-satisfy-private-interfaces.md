---
title: CA2119：密封满足私有接口的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: af41fc5576cbcd56589680d99c0cd5c0dfd6e6f1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664773"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119：密封满足私有接口的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 可继承的公共类型提供 `internal` `Friend` （Visual Basic）接口中的可重写的方法实现。

## <a name="rule-description"></a>规则说明
 接口方法具有公共可访问性，实现类型不能对其进行更改。 内部接口创建一个协定，该协定不应在定义接口的程序集的外部实现。 使用 `virtual` （在 Visual Basic 中 `Overridable`）修饰符实现内部接口的方法的公共类型允许该方法被位于程序集外部的派生类型重写。 如果定义程序集中的第二个类型调用方法并且需要仅限内部的协定，则在执行外部程序集中重写的方法时，行为可能会受到影响。 这会产生安全漏洞。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用以下方法之一阻止在程序集外重写方法：

- 使声明类型 `sealed` （`NotInheritable` Visual Basic）。

- 将声明类型的可访问性更改为 `internal` （`Friend` Visual Basic）。

- 删除声明类型中的所有公共构造函数。

- 无需使用 `virtual` 修饰符即可实现此方法。

- 显式实现方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果仔细检查后，如果在程序集外重写方法，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了与此规则冲突的类型 `BaseImplementation`。

 [!code-cpp[FxCop.Security.SealMethods1#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cpp/FxCop.Security.SealMethods1.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cs/FxCop.Security.SealMethods1.cs#1)]
 [!code-vb[FxCop.Security.SealMethods1#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/vb/FxCop.Security.SealMethods1.vb#1)]

## <a name="example"></a>示例
 下面的示例利用上一个示例的虚方法实现。

 [!code-cpp[FxCop.Security.SealMethods2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cpp/FxCop.Security.SealMethods2.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cs/FxCop.Security.SealMethods2.cs#1)]
 [!code-vb[FxCop.Security.SealMethods2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/vb/FxCop.Security.SealMethods2.vb#1)]

## <a name="see-also"></a>请参阅
 [接口](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)[接口](https://msdn.microsoft.com/library/61b06674-12c9-430b-be68-cc67ecee1f5b)
