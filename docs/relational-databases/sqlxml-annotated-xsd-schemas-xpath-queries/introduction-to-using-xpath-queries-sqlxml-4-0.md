---
title: XPath クエリの使用の概要 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f82c330e2d18f05d0f358171a4ffeabc63ac9c3c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246593"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>XPath クエリの使用について (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML パス言語 (XPath) クエリは、URL の一部として、またはテンプレート内で指定できます。 この結果のフラグメントの構造はマッピング スキーマによって決定され、値はデータベースから取得されます。 このプロセスは、CREATE VIEW ステートメントを使用してビューを作成し、そのビューに対して SQL クエリを記述するのと概念的には同じです。  
  
> [!NOTE]  
>  SQLXML 4.0 の XPath クエリを理解するには、XML ビューと、それに関連するテンプレートやマッピング スキーマなどの概念について理解している必要があります。 詳細については、「 [&#40;SQLXML 4.0&#41;の注釈付き XSD スキーマの概要](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)」および「WORLD WIDE WEB コンソーシアム (W3C) で定義されている XPath 標準」を参照してください。  
  
 XML ドキュメントは、要素ノード、属性ノード、テキスト ノードなどのノードで構成されます。 たとえば、次の XML ドキュメントを考えてみます。  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 このドキュメントでは、 ** \<Customer>** が要素ノード、 **cid**が属性ノード、 **"Important"** がテキストノードです。  
  
 XPath は、XML ドキュメントからノード セットを選択するときに使用できるグラフ ナビゲーション言語です。 XPath の各演算子では、前の XPath 演算子によって選択されたノード セットに基づいて、ノード セットを選択します。 たとえば、 ** \<顧客>** ノードのセットを指定した場合、XPath では、 **date**属性値が **"7/14/1999"** であるすべて** \<の注文>** ノードを選択できます。 結果のノード セットには、注文日が 1999 年 7 月 14 日となっているすべての注文が含まれます。  
  
 XPath 言語は W3C (World Wide Web Consortium) によって標準のナビゲーション言語として定義されています。 SQLXML 4.0 は、W3C XPath 仕様のサブセットを実装します。 http://www.w3.org/TR/1999/PR-xpath-19991008.htmlこのサブセットは、にあります。  
  
 次に、W3C XPath 実装と SQLXML 4.0 実装の主な違いを示します。  
  
-   **ルート クエリ**  
  
     SQLXML 4.0 では、ルート クエリ (/) はサポートされません。 すべての XPath クエリは、スキーマ内の最上位レベル** \<の ElementType>** から開始する必要があります。  
  
-   **エラーの報告**  
  
     W3C XPath 仕様では、エラー状態は定義されていません。 ノードの選択に失敗した XPath クエリでは、空のノード セットが返されます。 SQLXML 4.0 では、さまざまな種類のエラー メッセージが返されます。  
  
-   **ドキュメント序数**  
  
     SQL XML 4.0 では、ドキュメント序数が必ずしも決まっていません。 そのため、ドキュメントの順序 (**次の例**を含む) を使用する数値述語と軸は実装されていません。  
  
     ドキュメント序数がないため、ノードの文字列値は、ノードが単一行の単一列にマップされる場合にのみ評価できます。 子要素を含む要素や IDREFS または NMTOKENS ノードは、文字列に変換できません。  
  
    > [!NOTE]  
    >  場合によっては、**リレーションシップ**注釈の**キーフィールド**の注釈またはキーによって、明確なドキュメント順序が生成されることがあります。 ただし、これはこれらの注釈を主に使用することではありません。詳細については、「 [sql: キーフィールドを使用したキー列の識別 &#40;sqlxml 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md) 」と「 [sql:&#41;4.0 &#40;Relationship を使用したリレーションシップの指定](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)」を参照してください。  
  
-   **データの種類**  
  
     SQLXML 4.0 では、XPath**文字列**、**数値**、および**ブール**データ型の実装に制限があります。 詳細については、「 [XPath データ型 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)」を参照してください。  
  
-   **クロス積クエリ**  
  
     SQLXML 4.0 では、`Customers[Order/@OrderDate=Order/@ShipDate]` などのクロス積 XPath クエリはサポートされません。 このクエリでは、任意の Order の OrderDate が任意の Order の ShipDate と等しいすべての Customer が選択されます。  
  
     ただし、SQLXML 4.0 では、`Customer[Order[@OrderDate=@ShippedDate]]` などのクエリはサポートされます。このクエリでは、任意の Order の OrderDate とその ShipDate が等しいすべての Customer が選択されます。  
  
-   **エラー処理とセキュリティ**  
  
     使用されるスキーマと XPath クエリ式によっては、一定の条件下において、[!INCLUDE[tsql](../../includes/tsql-md.md)] エラーがユーザーに表示されることがあります。  
  
 以下に示す表では、この分野に関する SQLXML 4.0 の XPath クエリの実装と W3C 仕様の違いを詳しく説明します。  
  
## <a name="supported-functionality"></a>サポートされる機能  
 次の表は、SQLXML 4.0 で実装されている XPath 言語の機能です。  
  
|機能|item|サンプル クエリへのリンク|  
|-------------|----------|----------------------------|  
|軸|**属性**、**子**、**親**、および**自己**軸|[XPath クエリでの軸の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|連続する述語や入れ子になった述語など、ブール値を使用する述語||[XPath クエリでの算術演算子の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|すべての関係演算子|=、! =、<、 \<=、>、>=|[XPath クエリでの関係演算子の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|算術演算子|+、-、*、div|[XPath クエリでの算術演算子の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|明示的な変換関数|**number ()**、 **string ()**、 **Boolean ()**|[XPath クエリでの明示的な変換関数の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|ブール演算子|AND、OR|[XPath クエリでのブール演算子の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Boolean 関数群|**true ()**、 **false ()**、 **not ()**|[XPath クエリでのブール関数の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|XPath 変数||[XPath クエリでの XPath 変数の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>サポートされない機能  
 次の表は、SQLXML 4.0 で実装されていない XPath 言語の機能です。  
  
|機能|item|  
|-------------|----------|  
|軸|**先祖**、**先祖、また**は self、**子孫**、**子孫、または自己 (//)**、**次**の**兄弟**、**名前空間**、**先行**、**前の兄弟**|  
|数値を使用する述語||  
|算術演算子|mod|  
|ノード関数|**先祖**、**先祖、また**は self、**子孫**、**子孫、または自己 (//)**、**次**の**兄弟**、**名前空間**、**先行**、**前の兄弟**|  
|文字列関数|**string ()**、 **concat ()**、**開始-with ()**、 **contains ()**、 **substring ()**、substring ( **)**、 **substring ()**、**文字列長 ()**、**正規化 (**)、**変換 ()**|  
|Boolean 関数群|**lang ()**|  
|数値関数|**sum ()**、 **floor ()**、**シーリング ()**、 **round ()**|  
|Union 演算子|&#124;|  
  
 テンプレートに XPath クエリを指定する場合には、次の動作に注意してください。  
  
-   XPath には、XML で特別な意味を持つ < や & などの文字を含めることができます (およびテンプレートは XML ドキュメントです)。 XML & エンコードを使用してこれらの文字をエスケープするか、URL に XPath を指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 での XPath クエリの使用](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
