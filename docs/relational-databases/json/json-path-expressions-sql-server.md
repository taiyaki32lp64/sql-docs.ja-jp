---
title: JSON パス式
ms.date: 01/23/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8f345576db61768d9afe8243dfe41801f68b2ac
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095731"
---
# <a name="json-path-expressions-sql-server"></a>JSON パス式 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 JSON オブジェクトのプロパティを参照するには、JSON パス式を使用します。  
  
 次の関数を呼び出すときに、パス式を指定する必要があります。  
  
-   **OPENJSON** を呼び出して、JSON データのリレーショナル ビューを作成します。 詳細については、「 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)」をご覧ください。  
  
-   **JSON_VALUE** を呼び出して、JSON テキストから値を抽出します。 詳細については、「 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)」をご覧ください。  
  
-   **JSON_QUERY** を呼び出して、JSON オブジェクトまたは配列を抽出します。 詳細については、「 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)」をご覧ください。  
  
-   **JSON_MODIFY** を呼び出して、JSON 文字列内のプロパティの値を更新します。 詳細については、「 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)」を参照してください。  

## <a name="parts-of-a-path-expression"></a>パス式の各部
 パス式には 2 つのコンポーネントがあります。  
  
1.  省略可能な [パス モード](#PATHMODE) (値は **lax** または **strict**)。  
  
2.  [パス](#PATH) 自体。  

##  <a name="PATHMODE"></a> Path mode  
 必要に応じて、パス式の先頭に **lax** または **strict**キーワードを指定してパス モードを宣言します。 既定値は **lax**です。  
  
-   **lax** モードでは、パス式にエラーが含まれている場合、関数は空の値を返します。 たとえば、値 **$.name** を要求するときに JSON テキストに **name** キーが含まれていない場合、関数は null を返しますが、エラーは発生しません。  
  
-   **strict** モードでは、パス式にエラーが含まれている場合、関数でエラーが発生します。  

次のクエリでは、パス式で `lax` モードが明示的に指定されています。

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 省略可能なパス モード宣言の後に、パス自体を指定します。  
  
-   ドル記号 (`$`) はコンテキスト アイテムを表します。  
  
-   プロパティのパスは、パス ステップのセットです。 パス ステップには、次の要素と演算子を含めることができます。  
  
    -   キー名。 たとえば、 `$.name` や `$."first name"`。 キー名がドル記号で始まるか、キー名にスペースなどの特殊文字が含まれている場合は、引用符で囲みます。   
  
    -   配列の要素。 たとえば、`$.product[3]` のようになります。 配列は 0 から始まります。  
  
    -   ドット演算子 (`.`) は、オブジェクトのメンバーを示します。 たとえば、`$.people[1].surname` では、`surname` は `people` の子です。
  
## <a name="examples"></a>使用例  
 このセクションの例では、次の JSON テキストを参照します。  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 次の表に、パス式の例をいくつか示します。  
  
|パス式|[値]|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name":"Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name":"John",  "surname":"Doe" },<br />   { "name":"Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>組み込み関数が重複するパスを処理する方法  
 たとえば、同じ名前の 2 つのキーが同じレベルにある場合など、JSON テキストに重複するプロパティが含まれる場合、**JSON_VALUE** および **JSON_QUERY** 関数はパスに一致する最初の値のみを返します。 重複するキーが含まれる JSON オブジェクトを解析してすべての値を取得するには、次の例に示すように **OPENJSON** を使用します。  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  
