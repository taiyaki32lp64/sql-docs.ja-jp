---
title: 複雑な名前を持つカスタム アセンブリの使用 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 31479ae9b460b6a660ec865e68e46afd912f49b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194089"
---
# <a name="using-strong-named-custom-assemblies"></a>複雑な名前を持つカスタム アセンブリの使用
  複雑な名前はアセンブリを識別します。この名前には、アセンブリのマニフェストに格納されたアセンブリのテキスト名、4 つの部分から成るバージョン番号、カルチャ情報 (指定されている場合)、公開キー、およびデジタル署名が含まれます。 複雑な名前は、共通言語ランタイム (CLR) にアセンブリを一意に識別し、バイナリの整合性を確保します。  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>AllowPartiallyTrustedCallersAttribute の使用  
 複雑な名前を持つアセンブリをレポートと一緒に使用するには、アセンブリの **AllowPartiallyTrustedCallers** 属性を使用する部分的に信頼されるコードが複雑な名前を持つアセンブリを呼び出すことを許可する必要があります。 **AllowPartiallyTrustedCallersAttribute** を使用すると、レポート デザイナーまたはレポート サーバーが複雑な名前を持つアセンブリをレポート式で呼び出すことを許可できます。 部分的に信頼されるコードが複雑な名前を持つアセンブリを呼び出すことを許可するには、アセンブリ属性ファイルに次のアセンブリ レベル属性を追加します。  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** は、アセンブリ レベルで複雑な名前を持つアセンブリによって適用された場合のみ有効です。 アセンブリ レベルでの属性適用の詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントの「属性の適用」を参照してください。  
  
> [!CAUTION]  
>  **AllowPartiallyTrustedCallersAttribute** が存在する場合は、既定の **FullTrustLinkDemand** セキュリティ チェックが行われないため、部分的に信頼される他のすべてのアセンブリからそのアセンブリを呼び出すことができます。 すべてのセキュリティ チェックは、クラス レベルやメソッド レベルの宣言セキュリティ属性を含め、明示的に指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
