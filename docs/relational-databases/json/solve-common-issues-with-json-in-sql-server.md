---
title: SQL Server での JSON に関する一般的な問題を解決する
ms.date: 07/07/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8dd50c08035690fd932dc717ae08d179b89b4ed2
ms.sourcegitcommit: a92fa97e7d3132ea201e4d86c76ac39cd564cd3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2019
ms.locfileid: "75325419"
---
# <a name="solve-common-issues-with-json-in-sql-server"></a>SQL Server での JSON に関する一般的な問題を解決する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 SQL Server での組み込み JSON サポートに関する一般的な質問に対する回答をこちらで見つけることができます。  
 
## <a name="for-json-and-json-output"></a>FOR JSON および JSON 出力

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH または FOR JSON AUTO?  
 **質問** 単一のテーブル上の単純な SQL クエリから JSON テキストの結果を作成する必要があります。 FOR JSON PATH および FOR JSON AUTO は、同じ出力を生成します。 これら 2 つのオプションのどちらを使用する必要がありますか。  
  
 **回答** FOR JSON PATH を使用します。 JSON の出力に違いはありませんが、AUTO モードは列を入れ子にするかどうかを確認する追加のロジックを適用します。 PATH を既定のオプションと見なします。  

### <a name="create-a-nested-json-structure"></a>入れ子になった JSON 構造の作成  
 **質問** 同じレベルで複数の配列を持つ複雑な JSON を生成する必要があります。 FOR JSON PATH では、パスを使用して入れ子になったオブジェクトを作成できます。また、FOR JSON AUTO では、テーブルごとに追加の入れ子になったレベルを作成します。 これら 2 つのオプションのどちらを使用しても、目的の出力を生成することができます。 既存のオプションが直接サポートしていないカスタムの JSON 形式を作成する方法はありますか。  
  
 **回答** JSON テキストを返す FOR JSON クエリを列式として追加することで、データ構造を作成できます。 また、JSON_QUERY 関数を使って、JSON を手動で作成することもできます。 次の例ではこれらの技法を示します。  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}') as t41  
FROM t1  
FOR JSON PATH  
```  
  
FOR JSON クエリまたは列式の JSON_QUERY 関数のすべての結果は、個別の入れ子になった JSON サブオブジェクトとして書式設定され、メインの結果に含まれます。  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>FOR JSON 出力内のダブルエスケープが指定された JSON を防ぐ  
 **質問** JSON テキストをテーブルの列に保存しました。 このテキストを FOR JSON の出力に含める必要があります。 しかしながら、FOR JSON では JSON 内のすべての文字をエスケープするため、次の例で示すように、入れ子になったオブジェクトではなく、JSON 文字列を取得しています。  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 このクエリの結果は、次のようになります。  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 この動作を回避する方法はありますか。 エスケープされたテキストではなく、JSON オブジェクトとして返される `{"day":23}` が必要です。  
  
 **回答** テキストの列またはリテラルに保存された JSON は、任意のテキストのように扱われます。 つまり、これは二重引用符で囲まれ、エスケープされます。 エスケープされない JSON オブジェクトとして返す場合は、次の例のように、JSON 列を JSON_QUERY 関数に引数として渡します。  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 省略可能な 2 番目のパラメーターのない JSON_QUERY は、結果として 1 番目の引数のみを返します。 JSON_QUERY は有効な JSON を常に返すため、FOR JSON は、この結果をエスケープする必要がないと認識します。

### <a name="json-generated-with-the-without_array_wrapper-clause-is-escaped-in-for-json-output"></a>WITHOUT_ARRAY_WRAPPER 句を使用して生成された JSON は、FOR JSON の出力でエスケープされます。  
 **質問** FOR JSON と WITHOUT_ARRAY_WRAPPER オプションを使用して、列式の書式設定を行おうとしています。  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 FOR JSON クエリによって返された文字列は、プレーン テキストとしてエスケープされているようです。 これは、WITHOUT_ARRAY_WRAPPER が指定されている場合にのみ発生します。 どうして JSON オブジェクトとして扱われず、エスケープされないで結果に含まれないのですか?  
  
 **回答** 内側の `FOR JSON` で `WITHOUT_ARRAY_WRAPPER` オプションを指定すると、結果の JSON テキストは必ずしも有効な JSON ではなくなります。 そのため、外側の `FOR JSON` では、これをプレーン テキストと見なし、文字列をエスケープします。 JSON の出力が有効であることが確実な場合は、次の例のように、`JSON_QUERY` 関数を使用してそれをラップし、正しく書式設定された JSON に昇格させます。  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>OPENJSON および JSON 入力

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>OPENJSON のある JSON テキストから入れ子になった JSON サブオブジェクトを返す  
 **質問** 明示的なスキーマを持つ OPENJSON を使用して、スカラー値、オブジェクトおよび配列の両方を含む、複雑な JSON オブジェクトの配列を開くことができません。 WITH 句内のキーを参照する場合、スカラー値のみが返されます。 オブジェクトと配列は、null 値として返されます。 オブジェクトまたは配列を JSON オブジェクトとして抽出する方法はありますか。  
  
 **回答** 列としてオブジェクトまたは配列を返す場合、次の例で示すように、列定義で AS JSON オプションを使用します。  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-json_value"></a>JSON_VALUE ではなく OPENJSON を使って長いテキスト値を返す
 **質問** 長いテキストを含む JSON テキストに説明キーがあります。 `JSON_VALUE(@json, '$.description')` が、値の代わりに NULL を返します。  
  
 **回答** JSON_VALUE は小さいスカラー値を返すように設計されています。 一般的に、この関数はオーバーフロー エラーの代わりに NULL を返します。 より長い値を返す場合は、次の例のように、NVARCHAR(MAX) 値をサポートする OPENJSON を使用します。  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-json_value"></a>JSON_VALUE ではなく OPENJSON を使って重複キーを処理する
 **質問** JSON テキストに重複するキーがあります。 JSON_VALUE は、パス上で見つかる最初のキーのみを返します。 同じ名前を持つすべてのキーを取得する方法はありますか。  
  
 **回答** 組み込みの JSON スカラー関数は、最初に出現する参照先のオブジェクトのみを返します。 複数のキーが必要な場合は、次の例で示すように、OPENJSON テーブル値関数を使用します。  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON には、互換性レベル 130 が必要です。  
 **質問** SQL Server 2016 で OPENJSON を実行しようとしていて、次のエラーが発生しています。  
  
 `Msg 208, Level 16, State 1 'Invalid object name OPENJSON'`  
  
 **回答** OPENJSON 関数は、互換性レベル 130 でのみ使用できます。 DB の互換性レベルが 130 より下の場合、OPENJSON は非表示になります。 他の JSON 関数は、すべての互換性レベルで使用できます。  
 
## <a name="other-questions"></a>その他の質問

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>JSON テキストに英数字以外の文字を含む参照キー  
 **質問** JSON テキストのキーに英数字以外の文字があります。 これらのプロパティを参照する方法はありますか。  
  
 **回答** JSON パスでその文字を引用符で囲む必要があります。 たとえば、「 `JSON_VALUE(@json, '$."$info"."First Name".value')` 」のように入力します。
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
