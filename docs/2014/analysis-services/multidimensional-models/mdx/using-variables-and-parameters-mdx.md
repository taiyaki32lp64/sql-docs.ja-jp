---
title: 変数とパラメーター (MDX) の使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eeb258266c489056994d8f78f80a6856602a174a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073711"
---
# <a name="using-variables-and-parameters-mdx"></a>変数とパラメーターの使用 (MDX)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]では、多次元式 (MDX) ステートメントをパラメーター化できます。 ステートメントをパラメーター化すれば、実行時にカスタマイズ可能な汎用ステートメントを作成できます。  
  
 パラメーター化されたステートメントを作成するときには、パラメーター名の前に @ 記号を付けることによってパラメーター名を識別します。 たとえば、@Year有効なパラメーター名になります。  
  
 MDX は、リテラルまたはスカラー値用のパラメーターだけをサポートします。 メンバー、セット、または組を参照するパラメーターを作成するには、 [StrToMember](/sql/mdx/strtomember-mdx) や [StrToSet](/sql/mdx/strtoset-mdx)などの関数を使う必要があります。  
  
 次の XML for Analysis (XMLA) の例で、@CountryNameパラメーター データを取得する顧客の国が含まれます。  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 OLE DB でこの機能を使用するには、`ICommandWithParameters` インターフェイスを使用します。 ADOMD.Net でこの機能を使用するには、 **AdomdCommand.Parameters** コレクションを使用します。  
  
## <a name="see-also"></a>関連項目  
 [MDX スクリプティングの基礎 &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
