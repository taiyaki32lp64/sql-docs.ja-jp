---
title: 挿入、更新、およびメンバー (XMLA) の削除 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98da3e0f7a9b61b178372d9b24b8b595ab6b6626
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727166"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>メンバーの挿入、更新、および削除 (XMLA)
  使用することができます、[挿入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)、[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)、および[ドロップ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)コマンドでは、XML for Analysis (XMLA) それぞれを挿入するには、更新、またはメンバーを書き込み許可ディメンションから削除します。 書き込み許可ディメンションの詳細については、次を参照してください。 [Write-Enabled ディメンション](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)します。  
  
## <a name="inserting-new-members"></a>新しいメンバーの挿入  
 `Insert` コマンドは、書き込み許可ディメンション内の指定された属性に新しいメンバーを挿入します。  
  
 `Insert` コマンドを作成する前に、挿入する新しいメンバーに関する以下の情報を確認しておく必要があります。  
  
-   新しいメンバーを挿入するディメンション。  
  
-   新しいメンバーを挿入するディメンションの属性。  
  
-   新しいメンバーの名前。ある場合は、名前の翻訳も含みます。  
  
-   新しいメンバーのキー。 属性で複合キーを使用する場合は、キーに複数の値が必要になることがあります。  
  
-   ディメンション内で他の属性として実装されていない属性プロパティがあれば、その値。 そのような属性プロパティには、単項演算子、翻訳、カスタム ロールアップ、カスタム ロールアップ プロパティ、およびスキップされたレベルなどがあります。  
  
 `Insert` コマンドのプロパティは、以下の 2 つだけです。  
  
-   [オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)プロパティで、メンバーが挿入されるのディメンションのオブジェクト参照が含まれています。 オブジェクト参照には、そのディメンションに関するデータベース識別子、キューブ識別子、およびディメンション識別子が含まれます。  
  
-   [属性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla)プロパティで、1 つ以上含む[属性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla)メンバーの挿入する属性を識別する要素。 各 `Attribute` 要素は、属性を識別し、その属性に追加する 1 つのメンバーの、名前、値、翻訳、単項演算子、カスタム ロールアップ、カスタム ロールアップ演算子、およびスキップされたレベルを指定します。  
  
    > [!NOTE]  
    >  `Attribute` 要素には、すべてのプロパティを含める必要があります。 そうでない場合、エラーが発生する可能性があります。  
  
## <a name="updating-existing-members"></a>既存のメンバーの更新  
 `Update` コマンドは、書き込み許可ディメンション内にある指定された属性内の既存のメンバーを、他の属性内の他のメンバーとの関係に基づいて更新します。 `Update` コマンドを使用すると、ディメンションに含まれる階層内の他のレベルにメンバーを移動することや、親属性によって定義される親子階層を再構成することができます。  
  
 `Update` コマンドを作成する前に、更新するメンバーに関する以下の情報を確認しておく必要があります。  
  
-   更新する既存のメンバーを含むディメンション。  
  
-   更新する既存のメンバーを含むディメンションの属性。  
  
-   既存のメンバーのキー。 属性で複合キーを使用する場合は、キーに複数の値が必要になることがあります。  
  
-   ディメンション内で他の属性として実装されていない属性プロパティがあれば、その値。 そのような属性プロパティには、単項演算子、翻訳、カスタム ロールアップ、カスタム ロールアップ プロパティ、およびスキップされたレベルなどがあります。  
  
 `Update` コマンドのプロパティは、以下の 3 つの必須プロパティだけです。  
  
-   `Object` プロパティ。メンバーを更新するディメンションへのオブジェクト参照が含まれます。 オブジェクト参照には、そのディメンションに関するデータベース識別子、キューブ識別子、およびディメンション識別子が含まれます。  
  
-   `Attributes` プロパティ。メンバーを更新するディメンションを識別するための 1 つ以上の `Attribute` 要素が含まれます。 `Attribute` 要素は、属性を識別し、その属性に関して更新する 1 つのメンバーの、名前、値、翻訳、単項演算子、カスタム ロールアップ、カスタム ロールアップ演算子、およびスキップされたレベルを指定します。  
  
    > [!NOTE]  
    >  `Attribute` 要素には、すべてのプロパティを含める必要があります。 そうでない場合、エラーが発生する可能性があります。  
  
-   [場所](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla)プロパティで、1 つ以上含む`Attribute`メンバーの更新する属性を制限する要素。 `Where`プロパティは、制限するために重要な`Update`メンバーの特定のインスタンスにコマンド。 場合、`Where`プロパティが指定されていない、指定されたメンバーのすべてのインスタンスが更新されます。 たとえば、3 人の顧客について、都市名を Redmond から Bellevue に変更したいとします。 都市名を変更するには、変更する City 属性のメンバーに対して、Customer 属性の 3 つのメンバーを識別する `Where` プロパティを指定する必要があります。 この `Where` プロパティを指定せずに `Update` コマンドを実行すると、都市名が現在 Redmond であるすべての顧客について、都市名が Bellevue に変更されます。  
  
    > [!NOTE]  
    >  新しいメンバーを除く、`Update`コマンドに含まれていない属性の属性のキー値で更新できる、`Where`句。 たとえば、ある顧客が更新されている場合には都市名を更新できません。それ以外の場合には、すべての顧客に関して都市名が変更されます。  
  
### <a name="updating-members-in-parent-attributes"></a>親階層のメンバーの更新  
 親の属性をサポートするために、`Update`省略可能なコマンド[MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)MovewithDescedants プロパティ。 `MoveWithDescendants` プロパティを true に設定すると、親メンバーの識別子が変更された場合に、その親メンバーの子孫も親メンバーと一緒に移動します。 この値が false に設定されている場合は、親メンバーを移動すると、その親メンバーの直接の子孫が親メンバーのあったレベルに昇格します。  
  
 親属性のメンバーを更新する場合、`Update` コマンドで他の属性のメンバーを更新することはできません。  
  
## <a name="dropping-existing-members"></a>既存のメンバーの削除  
 `Drop` コマンドを作成する前に、削除するメンバーに関する以下の情報を確認しておく必要があります。  
  
-   削除する既存のメンバーを含むディメンション。  
  
-   削除する既存のメンバーを含むディメンションの属性。  
  
-   削除する既存のメンバーのキー。 属性で複合キーを使用する場合は、キーに複数の値が必要になることがあります。  
  
 `Drop` コマンドのプロパティは、以下の 2 つの必須プロパティだけです。  
  
-   `Object` プロパティ。メンバーを破棄するディメンションへのオブジェクト参照が含まれます。 オブジェクト参照には、そのディメンションに関するデータベース識別子、キューブ識別子、およびディメンション識別子が含まれます。  
  
-   `Where` プロパティ。メンバーを削除するディメンションを制限するための 1 つ以上の `Attribute` 要素が含まれます。 `Where` プロパティは、`Drop` コマンドをメンバーの特定のインスタンスに制限する場合に不可欠です。 `Where` プロパティが指定されない場合、特定のメンバーのすべてのインスタンスが削除されます。 たとえば、Redmond から 3 人の顧客を削除したいとします。 これらの顧客を削除するには、Customer 属性で削除対象の 3 つのメンバーと、3 人の顧客を削除する City 属性の Redmond メンバーの両方を識別する `Where` プロパティを指定する必要があります。 `Where` プロパティで City 属性の Redmond メンバーだけが指定されている場合、Redmond に関連付けられているすべての顧客が `Drop` コマンドによって削除されます。 `Where` プロパティで Customer 属性の 3 つのメンバーだけが指定されている場合、3 人の顧客に関して、`Drop` コマンドによって全体が削除されます。  
  
    > [!NOTE]  
    >  `Attribute`に含まれる要素を`Drop`のみコマンドを含める必要があります、`AttributeName`と`Keys`プロパティ。 そうでない場合、エラーが発生する可能性があります。  
  
### <a name="dropping-members-in-parent-attributes"></a>親階層のメンバーの削除  
 設定、 [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla)プロパティは親メンバーの子孫が親メンバーを削除するかも示します。 この値が false に設定されている場合は、その親メンバーの直接の子孫が、親メンバーのあったレベルに昇格します。  
  
> [!IMPORTANT]  
>  親メンバーとその子孫の両方を削除するためにユーザーに必要な権限は、親メンバーに対する削除権限だけです。 ユーザーが子孫に対する削除権限を持っている必要はありません。  
  
## <a name="see-also"></a>参照  
 [Drop 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [要素を挿入&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Update 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [定義するオブジェクトを識別したり&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
