---
title: ユーザー定義メンバー プロパティ (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ead5a45bf163ca4e7998c30ab5c83f94cca9075b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074260"
---
# <a name="user-defined-member-properties-mdx"></a>ユーザー定義メンバー プロパティ (MDX)
  属性リレーションシップとして、ディメンション内の指定されたレベルにユーザー定義メンバー プロパティを追加できます。 ユーザー定義メンバー プロパティは、階層の `(All)` レベル、または階層そのものには追加できません。  
  
## <a name="creating-user-defined-member-properties"></a>ユーザー定義メンバー プロパティの作成  
 以下のように、ユーザー インターフェイスを使用して、またはプログラムによって、サーバー ベースのディメンションまたはキューブにユーザー定義メンバー プロパティを追加できます。  
  
-   ユーザー インターフェイスを使用してユーザー定義メンバー プロパティを追加するには、 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]でディメンション デザイナーを使用します。 詳細については、「 [属性リレーションシップの定義](../attribute-relationships-define.md)」を参照してください。  
  
-   プログラムによってユーザー定義メンバー プロパティを追加するには、アプリケーションで Analysis Manager Objects (AMO) を使用するか、XML for Analysis (XMLA) と Analysis Services Scripting Language (ASSL) を組み合わせて使用できます。 詳細については、「 [属性リレーションシップ](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」を参照してください。  
  
## <a name="retrieving-user-defined-member-properties"></a>ユーザー定義メンバー プロパティの取得  
 いずれかを使用してユーザー定義メンバー プロパティを取得することができます、`PROPERTIES`キーワードまたは[プロパティ](/sql/mdx/properties-mdx)関数。  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>PROPERTIES キーワードを使用したユーザー定義メンバー プロパティの取得  
 次に示すように、ユーザー定義メンバー プロパティを取得する構文は、固有レベル メンバー プロパティを取得する構文と同様です。  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 `PROPERTIES` キーワードは、軸を指定するセット式の後に指定します。 たとえば、次の MDX クエリの `PROPERTIES` キーワードは `List Price` および `Dealer Price` ユーザー定義メンバー プロパティを取得するもので、1 月に販売された製品を示すセット式の後に指定されています。  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>Properties 関数を使用したユーザー定義メンバー プロパティの取得  
 別の方法として、`Properties` 関数を使ってカスタム メンバー プロパティにアクセスすることもできます。 たとえば、次の MDX クエリでは、`WITH` キーワードを使用して、`List Price` メンバー プロパティで構成される計算されるメンバーを作成します。  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 計算されるメンバーの作成方法の詳細については、「[MDX での計算されるメンバーの作成 &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [メンバー プロパティの使用 &#40;MDX&#41;](mdx-member-properties.md)   
 [プロパティ &#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
