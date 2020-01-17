---
title: FOR XML での AUTO モードの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e6464fee5779e35559b6eca23981aa09312aeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193265"
---
# <a name="use-auto-mode-with-for-xml"></a>FOR XML での AUTO モードの使用
  「 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)」で説明したように、AUTO モードを使用すると、入れ子構造の XML 要素としてクエリ結果が返されます。 AUTO モードでは、クエリ結果から生成される XML の構造はあまり制御されません。 AUTO モードのクエリは、単純な階層を生成する場合に役立ちます。 ただし、 [FOR XML での EXPLICIT モードの使用](use-explicit-mode-with-for-xml.md) や [FOR XML での PATH モードの使用](use-path-mode-with-for-xml.md) により、クエリ結果から XML の構造を決定するときに、より厳密な制御や高い柔軟性を実現できます。  
  
 FROM 句の各テーブルは XML 要素として表され、そのうち少なくとも 1 列が SELECT 句のリストに含められます。 FOR XML 句で省略可能な ELEMENTS オプションを指定すると、SELECT 句のリストに含められる列は属性またはサブ要素にマップされます。  
  
 生成される XML 内の要素が入れ子になった XML 階層は、SELECT 句で指定されている列で識別されるテーブルの順序に基づきます。 そのため、SELECT 句で列名を指定する順序は重要です。 先頭、つまり識別された左端のテーブルにより、生成される XML ドキュメント内の最上位要素が形成されます。 SELECT ステートメント内の列で識別された左から 2 番目のテーブルにより、最上位要素内のサブ要素が形成されます。以降についても同様です。  
  
 SELECT 句のリストに含まれている列名が、SELECT 句でそれ以前に指定した列によって既に識別されたテーブルに含まれている場合、その列は、階層の新しいレベルを開くのではなく、既に作成されている要素の属性として追加されます。 ELEMENTS オプションを指定している場合は、その列が属性として追加されます。  
  
 たとえば、次のクエリを実行するとします。  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 結果の一部を次に示します。  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 SELECT 句では、次の点に注意してください。  
  
-   CustomerID は Cust テーブルを参照します。 そのため、<`Cust`> 要素が作成され、CustomerID がその要素の属性として追加されます。  
  
-   次に、OrderHeader.CustomerID、OrderHeader.SaleOrderID、および OrderHeader.Status の 3 列が、OrderHeader テーブルを参照します。 そのため、<`OrderHeader`> 要素が <`Cust`> 要素のサブ要素として追加され、OrderHeader テーブルを参照する 3 列が <`OrderHeader`> の属性として追加されます。  
  
-   次に、Cust.CustomerType 列が、Cust.CustomerID 列で既に識別された Cust テーブルを再び参照します。 このため、新しい要素は作成されません。 この場合、以前作成した <`Cust`> 要素に CustomerType 属性が追加されます。  
  
-   クエリでは、テーブル名の別名が指定されます。 これらの別名は、対応する要素名として示されます。  
  
-   1 つの親のすべての子をグループ化するには、ORDER BY を指定する必要があります。  
  
 次のクエリは、SELECT 句で OrderHeader テーブルの列が指定されてから Cust テーブルの列が指定されている点を除いて、上記のクエリと同様です。 そのため、最初の <`OrderHeader`> 要素が作成されてから、その要素に <`Cust`> 子要素が追加されています。  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 結果の一部を次に示します。  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 FOR XML 句に ELEMENTS オプションを追加すると、要素中心の XML が返されます。  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 結果の一部を次に示します。  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 このクエリでは、\<Cust> 要素の作成時に CustomerID の値が行ごとに比較されます。これは、CustomerID がテーブルの主キーであるためです。 CustomerID がテーブルの主キーとして識別されない場合、列のすべての値 (このクエリでは CustomerID、CustomerType) が行ごとに比較されます。 値が異なる場合は、新しい \<Cust> 要素が XML に追加されます。  
  
 これらの列の値を比較するとき、比較するいずれかの列が **text**型、 **ntext**型、 **image**型、または **xml**型の場合は、FOR XML では値が同じ場合でも値が異なると想定され比較されません。 これは、ラージ オブジェクトの比較がサポートされていないためです。 選択した行ごとに、要素が結果に追加されます。 **(n)varchar(max)** 型および **varbinary(max)** 型の列は比較されることに注意してください。  
  
 集計列や計算列の場合と同様に、SELECT 句内の列を FROM 句内で識別されるいずれかのテーブルと関連付けることができない場合、その列がリストに見つかった時点で最も深い入れ子レベルの XML ドキュメントに追加されます。 このような列が SELECT 句内の最初の列の場合は、最上位の要素に追加されます。  
  
 SELECT 句にアスタリスク (*) ワイルドカード文字を指定すると、クエリ エンジンから行が返される順序に基づいて上記の説明と同じ方法で入れ子が決定されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のトピックでは、AUTO モードの詳細について説明します。  
  
-   [BINARY BASE64 オプションの使用](use-the-binary-base64-option.md)  
  
-   [返される XML を構造化する際の AUTO モード ヒューリスティック](auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [例: AUTO モードの使用](examples-using-auto-mode.md)  
  
## <a name="see-also"></a>参照  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
