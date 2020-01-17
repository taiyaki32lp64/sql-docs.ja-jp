---
title: XQueries リレーショナル データの処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: ed4583b30ed1e4538a36079f9f7794704b819cda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946169"
---
# <a name="xqueries-handling-relational-data"></a>リレーショナル データを処理する XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  に対して XQuery を指定する、 **xml**型の列または変数のいずれかを使用して、 [XML データ型メソッド](../t-sql/xml/xml-data-type-methods.md)します。 以下の**query()** 、 **value()** 、 **exist()** 、または**modify()** します。 XQuery は、XML を生成するクエリで識別される XML インスタンスに対して実行されます。  
  
 XQuery の実行によって生成される XML には、他の Transact-SQL 変数や行セット列から取得される値を含めることができます。 SQL Server では、XML 以外のリレーショナル データを結果の XML にバインドするために、XQuery 拡張として次の擬似関数が用意されています。  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 XQuery を指定するときに、これらの XQuery 拡張機能を使用することができます、 **query()** のメソッド、 **xml**データ型。 結果として、 **query()** メソッド XML および以外のデータを結合する XML を生成することができます-**xml**データ型。  
  
 使用する場合に、これらの関数を使用することもできます、 **xml**データ型のメソッド**modify()** 、 **value()** 、 **query()** 、および**exist()** XML 内部のリレーショナル値を公開します。  
  
 詳細については、次を参照してください。 [sql:column() 関数 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)と[sql:variable() 関数 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)します。  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML の構築&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
