---
title: メンバー プロパティ (MDX) の使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c0326d45af68db966f120fa12e35eb59f30becc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074159"
---
# <a name="using-member-properties-mdx"></a>メンバー プロパティの使用 (MDX)
  メンバー プロパティは、各組内の各メンバーに関する基本的な情報を対象とします。 基本的な情報には、メンバー名、親レベル、子の数などが含まれます。 メンバー プロパティは特定レベルのすべてのメンバーで使用できます。 編成の点では、メンバー プロパティは 1 つのディメンション上に格納され、ディメンション別に編成されるデータとして扱われます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、メンバー プロパティを属性リレーションシップと呼んでいます。 詳細については、「 [属性リレーションシップ](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」を参照してください。  
  
 メンバー プロパティには、 *固有* プロパティと *カスタム*プロパティがあります。  
  
 固有メンバー プロパティ  
 すべてのメンバーで、固有メンバー プロパティ (たとえば書式設定済みのメンバーの値など) がサポートされます。一方、ディメンションやレベルには、追加の固有ディメンション メンバー プロパティや追加の固有レベル メンバー プロパティ (たとえばメンバー ID など) が用意されています。  
  
 詳細については、「[固有メンバー プロパティ (MDX)](mdx-member-properties-intrinsic-member-properties.md)」を参照してください。  
  
 ユーザー定義メンバー プロパティ  
 多くの場合、メンバーには追加のプロパティが関連付けられます。 たとえば、製品レベルには、各製品の SKU、SRP、重さ、および量のプロパティが用意されているかもしれません。 これらのプロパティはメンバーではありませんが、製品レベルのメンバーに関する追加情報を含んでいます。  
  
 詳細については、「[ユーザー定義メンバー プロパティ (MDX)](mdx-member-properties-user-defined-member-properties.md)」を参照してください。  
  
 使用すると、両方の組み込みとユーザー定義メンバー プロパティを取得できる、`PROPERTIES`キーワードまたは[プロパティ](/sql/mdx/properties-mdx)関数。  
  
## <a name="using-the-properties-keyword"></a>PROPERTIES キーワードの使用  
 `PROPERTIES` キーワードを使用して、特定の軸ディメンションに対して使用するメンバー プロパティを指定します。 `PROPERTIES`内でキーワードが埋め込まれています、`<axis specification>`句は MDX の[選択](/sql/mdx/mdx-data-manipulation-select)ステートメント。  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 `<axis_specification>` 句には、以下の構文に示すように、オプションの `<dim_props>` 句が含まれています。  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  `<set>` 値と `<axis_name>` 値の詳細については、「[クエリ軸の内容の指定 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)」を参照してください。  
  
 `<dim_props>` 句によって、`PROPERTIES` キーワードを使用したディメンション、レベル、およびメンバー プロパティのクエリが実行可能になります。 `<dim_props>` 句の構文は次のとおりです。  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 `<property>` 構文のブレークダウンは、クエリの対象となるプロパティに応じて変わります。  
  
-   状況に依存する固有メンバー プロパティには、その前にディメンション名またはレベル名を指定する必要があります。 ただし、状況に依存しない固有メンバー プロパティはディメンション名やレベル名で修飾できません。 使用する方法についての詳細、`PROPERTIES`固有メンバー プロパティを持つキーワードを参照してください[固有メンバー プロパティ&#40;MDX&#41;](mdx-member-properties-intrinsic-member-properties.md)します。  
  
-   ユーザー定義メンバー プロパティの前には、そのプロパティが存在しているレベルの名前を指定する必要があります。 使用する方法についての詳細、`PROPERTIES`ユーザー定義メンバー プロパティを持つキーワードを参照してください[ユーザー定義メンバー プロパティ&#40;MDX&#41;](mdx-member-properties-user-defined-member-properties.md)します。  
  
## <a name="see-also"></a>参照  
 [プロパティ値の作成および使用 (MDX)](../../creating-and-using-property-values-mdx.md)  
  
  
