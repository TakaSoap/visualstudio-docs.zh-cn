---
title: 'CA1055: URI 返回值不应是字符串 |Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1055
- UriReturnValuesShouldNotBeStrings
helpviewer_keywords:
- UriReturnValuesShouldNotBeStrings
- CA1055
ms.assetid: 40e39873-7872-4988-8195-9eb0ade9ece0
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5fccccdef16d29e1dcc890c7799a8cb8a4486288
ms.sourcegitcommit: 99d097d82ee4f9eff6f588e5ebb6b17d8f724b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2018
ms.locfileid: "47587679"
---
# <a name="ca1055-uri-return-values-should-not-be-strings"></a>CA1055：URI 返回值不应是字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[CA1055: URI 返回值不应是字符串](https://docs.microsoft.com/visualstudio/code-quality/ca1055-uri-return-values-should-not-be-strings)。

|||
|-|-|
|TypeName|UriReturnValuesShouldNotBeStrings|
|CheckId|CA1055|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法的名称包含"uri"、"Uri"、"urn"、"Urn"、"url"或"Url"，并且该方法返回一个字符串。

## <a name="rule-description"></a>规则说明
 此规则将方法名称拆分为令牌基于 Pascal 大小写约定，并检查每个令牌等于"uri"、"Uri"、"urn"、"Urn"、"url"或"Url"。 如果没有匹配项，该规则将假定该方法返回的统一资源标识符 (URI)。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 <xref:System.Uri?displayProperty=fullName>类以安全的方式提供这些服务。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将返回类型更改为<xref:System.Uri>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果返回值不表示一个 URI。

## <a name="example"></a>示例
 下面的示例演示一种类型， `ErrorProne`，这违反了此规则和一个类型， `SaferWay`，满足该规则。

 [!code-cpp[FxCop.Design.UriNotString#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cpp/FxCop.Design.UriNotString.cpp#1)]
 [!code-csharp[FxCop.Design.UriNotString#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cs/FxCop.Design.UriNotString.cs#1)]
 [!code-vb[FxCop.Design.UriNotString#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/vb/FxCop.Design.UriNotString.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1056：URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054：URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA2234：传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1057：字符串 URI 重载调用 System.Uri 重载](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)


