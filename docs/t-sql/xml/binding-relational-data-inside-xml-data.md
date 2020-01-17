---
title: XML データ内部のリレーショナル データのバインド | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9a2253165045d74f669c52d0247b716e5576e8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051334"
---
# <a name="binding-relational-data-inside-xml-data"></a>XML データ内部のリレーショナル データのバインド
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)を **xml** データ型変数または列に対して指定できます。 たとえば、[query&#40;&#41; Method &#40;xml Data Type&#41;](../../t-sql/xml/query-method-xml-data-type.md) では、XML インスタンスに対して指定した XQuery が実行されます。 この方法で XML を構築するときに、XML 以外の型の列の値や Transact-SQL 変数を使用することもできます。 この処理を、XML 内部のリレーショナル データのバインドと呼びます。  
  
 XML 内部の XML 以外のリレーショナル データをバインドするために、SQL Server データベース エンジンには次の擬似関数が用意されています。  
  
-   [sql:column&#40;&#41; Function &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md)。この関数を使用すると、リレーショナル列の値を XQuery 式または XML DML 式で使用できます。  
  
-   [sql:variable&#40;&#41; 関数 &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md) . この関数を使用すると、SQL 変数の値を XQuery 式または XML DML 式で使用できます。  
  
 XML 内部でリレーショナル値を公開するときは、常に、**xml** データ型のメソッドと上記の関数を併用できます。  
  
 **xml** 型の列や変数、CLR ユーザー定義型、datetime、smalldatetime、**text**、**ntext**、**sql_variant**、および **image** の各型のデータを参照する場合は、これらの関数は使用できません。  
  
 また、このバインドは読み取り専用です。 つまり、これらの関数を使用する列には、データを書き込めません。 たとえば、sql:variable("\@x")="*some expression*" は使用できません。  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>例:sql:variable() を使用した複数の領域にまたがるクエリ  
 次の例では、**sql:variable()** を使用してアプリケーションでクエリをパラメーター化できるようにする方法を示します。 ISBN は、SQL 変数 @isbn を使用して渡されます。 定数を **sql:variable()** に置き換えたことにより、ISBN が 0-7356-1588-2 の書籍だけでなく、どの ISBN でも検索できます。  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** も同様に使用できますが、より多くの利点があります。 コストベースのクエリ オプティマイザーの判断により、効率を上げるために列のインデックスが使用される場合があります。 また、昇格したプロパティが計算列に保存される場合があります。  
  
## <a name="see-also"></a>参照  
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)  
  
  
