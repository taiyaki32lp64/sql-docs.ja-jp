---
title: OPENXML での value() メソッドと nodes() メソッドの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a511e977975ad0e23c9cf553de000b32bad24e69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039139"
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>OPENXML での value() メソッドと nodes() メソッドの使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **SELECT** 句で **xml** データ型に **value()** メソッドを複数回使用すると、抽出した値の行セットを生成できます。 **nodes()** メソッドは、追加のクエリに使用するために選択した各ノードの内部参照を生成します。 **nodes()** メソッドと **value()** メソッドを併用すると、行セットに複数の列があるとき、および行セット生成のためのパス式が複雑なときに、効率的に行セットを生成できます。  
  
 **nodes()** メソッドによって特別な **xml** データ型のインスタンスが生成され、それぞれのインスタンスのコンテキストは選択された個別のノードに設定されます。 このような XML インスタンスは、**query()** メソッド、**value()** メソッド、**nodes()** メソッド、および **exist()** メソッドをサポートし、**count(\*)** 集計で使用できます。 それ以外の使用方法ではエラーが発生します。  
  
## <a name="example-using-nodes"></a>例:nodes() の使用  
 名が "David" ではない著者の姓と名を抽出するとします。 2 つの列 FirstName および LastName から構成される行セットとしてこの情報を抽出します。 そのためには次に示すように、 **nodes()** メソッドと **value()** メソッドを使用します。  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 この例では、 `nodes('//author')` により各 XML インスタンスの `<author>` 要素への参照が格納された行セットが生成されます。 その参照について **value()** メソッドを評価することで、著者の姓および名を取得します。  
  
 SQL Server 2000 には、 **OpenXml()** を使用して XML インスタンスから行セットを生成する機能があります。 行セットにリレーショナル スキーマを指定し、その中の列に XML インスタンス内の値をどのようにマップするかを指定できます。  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>例:xml データ型での OpenXml() の使用  
 上記の例のクエリは、 **OpenXml()** を使用して次のように書き換えることができます。 そのためには、各 XML インスタンスを読み取って XML 変数に代入し、OpenXML に渡すカーソルを作成します。  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** によりメモリ内表現が作成され、クエリ プロセッサの代わりに作業テーブルが使用されます。 この関数は XQuery エンジンではなく MSXML Version 3.0 の XPath Version 1.0 プロセッサを使用します。 同一の XML インスタンスであっても、 **OpenXml()** の複数の呼び出しで作業テーブルを共有することはありません。 このため、スケーラビリティが制限されます。 **OpenXml()** を使用すると、WITH 句を指定しない場合に XML データのエッジ テーブル形式にアクセスできます。 また、別の "オーバーフロー" 列内の残りの XML 値を使用できます。  
  
 **nodes()** 関数と **value()** 関数を組み合わせると、XML インデックスを効果的に使用できます。 つまり、 **OpenXml**よりもスケーラビリティに優れています。  
  
## <a name="see-also"></a>参照  
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
