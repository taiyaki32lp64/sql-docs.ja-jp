---
title: FOR XML を使用した行セットからの XML の生成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b89a9efa3a034b9310384cc63a9b4c0c93ab8717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986451"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>FOR XML を使用した行セットからの XML の生成
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  新しい **TYPE** ディレクティブを指定した FOR XML を使用することで、 **xml** データ型のインスタンスを行セットから生成できます。  
  
 結果は **xml** データ型の列、変数、またはパラメーターに代入できます。 また、FOR XML を入れ子にして階層構造を作成することもできます。 入れ子にした FOR XML は FOR XML EXPLICIT よりも記述が容易ですが、階層が深いとパフォーマンスが低下する場合があります。 FOR XML には新しい PATH モードも導入されています。 この新しいモードで、列の値が現れる XML ツリーのパスを指定します。  
  
 新しい **FOR XML TYPE** ディレクティブを使用すると、リレーショナル データの読み取り専用の XML ビューを SQL 構文で定義できます。 このビューには、次の例で示すように SQL ステートメントおよびそれに埋め込まれた XQuery を使用してクエリを実行できます。 この SQL ビューをストアド プロシージャで参照することもできます。  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>例: 生成された xml データ型を返す SQL ビュー  
 次の SQL ビュー定義により、リレーショナル列 pk および XML 列から取得した著者氏名の XML ビューが作成されます。  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 V ビューには、1 列の XML 型の列 xmlVal から構成される 1 行が含まれます`.`通常の **xml** データ型のインスタンスと同様にクエリを実行できます。 たとえば、次のクエリは名が "David" の著者を返します。  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 SQL ビュー定義は、注釈付きスキーマを使用して作成する XML ビューと似ている部分があります。 しかし、両者には重大な違いがあります。 SQL ビュー定義は読み取り専用であり、埋め込みの XQuery で操作する必要があります。 XML ビューは、注釈付きスキーマを使用して作成します。 また、SQL ビューが XQuery 式を適用する前に XML の結果を具体化するのに対し、XML ビューへの XPath クエリは基になるテーブルで SQL クエリを評価します。  
  
## <a name="see-also"></a>参照  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
