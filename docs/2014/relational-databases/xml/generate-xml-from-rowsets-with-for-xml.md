---
title: FOR XML を使用した行セットからの XML の生成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 181d07e187c6b1091d38ebbe0018c61ae856caf3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204988"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>FOR XML を使用した行セットからの XML の生成
  生成することができます、`xml`新しいを FOR XML を使用して行セットからのデータ型のインスタンス**型**ディレクティブ。  
  
 結果に割り当てることができます、`xml`データ型の列、変数、またはパラメーター。 また、FOR XML を入れ子にして階層構造を作成することもできます。 入れ子にした FOR XML は FOR XML EXPLICIT よりも記述が容易ですが、階層が深いとパフォーマンスが低下する場合があります。 FOR XML には新しい PATH モードも導入されています。 この新しいモードで、列の値が現れる XML ツリーのパスを指定します。  
  
 新しい **FOR XML TYPE** ディレクティブを使用すると、リレーショナル データの読み取り専用の XML ビューを SQL 構文で定義できます。 このビューには、次の例で示すように SQL ステートメントおよびそれに埋め込まれた XQuery を使用してクエリを実行できます。 この SQL ビューをストアド プロシージャで参照することもできます。  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>例: 生成された xml データ型を返す SQL ビュー  
 次の SQL ビュー定義により、リレーショナル列 pk および XML 列から取得した著者氏名の XML ビューが作成されます。  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 V ビューには、XML 型の 1 つの xmlval 単一行が含まれています。`.` 、通常のようにクエリできる`xml`データ型のインスタンス。 たとえば、次のクエリは名が "David" の著者を返します。  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 SQL ビュー定義は、注釈付きスキーマを使用して作成する XML ビューと似ている部分があります。 しかし、両者には重大な違いがあります。 SQL ビュー定義は読み取り専用であり、埋め込みの XQuery で操作する必要があります。 XML ビューは、注釈付きスキーマを使用して作成します。 また、SQL ビューが XQuery 式を適用する前に XML の結果を具体化するのに対し、XML ビューへの XPath クエリは基になるテーブルで SQL クエリを評価します。  
  
## <a name="see-also"></a>参照  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
