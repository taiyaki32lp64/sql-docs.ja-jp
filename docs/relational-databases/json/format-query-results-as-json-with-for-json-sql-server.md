---
title: FOR JSON を使用してクエリ結果を JSON として書式設定する
ms.date: 06/06/2019
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43e9b416885a5cbd1239b0694ffc3613b7509186
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095814"
---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>FOR JSON を使用してクエリ結果を JSON として書式設定する (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

クエリ結果を JSON として書式設定するか、SQL Server のデータを JSON としてエクスポートするには、**FOR JSON** 句を **SELECT** ステートメントに追加します。 **FOR JSON** 句を使用して、JSON 出力の書式設定をアプリから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に委任することによって、クライアント アプリケーションを簡素化します。
  
 **FOR JSON** 句を使用すると、JSON 出力の構造を明示的に指定したり、SELECT ステートメントの構造によって出力を決定したりできます。  
  
-   JSON 出力の形式を継続して完全に制御するには、**FOR JSON PATH** を使用します。 ラッパー オブジェクトを作成して、複雑なプロパティを入れ子にすることができます。  
  
-   SELECT ステートメントの構造に基づいて JSON 出力を自動的に形式設定するには、**FOR JSON AUTO** を使用します。  
  
**FOR JSON** 句とその出力を使用した **SELECT** ステートメントの例を次に示します。
  
 ![JSON の](../../relational-databases/json/media/jsonslides2forjson.png)
  
## <a name="option-1---you-control-output-with-for-json-path"></a>オプション 1 - FOR JSON PATH でユーザーが出力を制御する
**PATH** モードではドット構文を使用できます。たとえば、ネストした出力を書式設定するには、`'Item.UnitPrice'` と指定します。  

**FOR JSON** 句で **PATH** モードを使用するサンプル クエリを次に示します。 次の例では、**ROOT** オプションを使用して名前付きのルート要素を指定しています。 
  
 ![FOR JSON 出力のフローの図](../../relational-databases/json/media/forjson-example1.png) 

### <a name="more-info-about-for-json-path"></a>FOR JSON PATH に関する詳細情報
詳細と例については、「[PATH モードで入れ子になった JSON 出力を書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)」を参照してください。

構文と使用法については、「 [FOR 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>オプション 2 - SELECT ステートメントで FOR JSON AUTO を使用して出力を制御する
**AUTO** モードでは、SELECT ステートメントの構造によって JSON 出力の形式が決まります。

既定では、 **null** 値は出力に含まれません。 **INCLUDE_NULL_VALUES** を使用してこの動作を変更できます。  

**FOR JSON** 句で **AUTO** モードを使用するサンプル クエリを以下に示します。

```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO;
```  

そして返された JSON を以下に示します。

```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```

### <a name="2b---example-with-join-and-null"></a>2.b - JOIN と NULL の例

以下の `SELECT...FOR JSON AUTO` の例には、`JOIN` されたテーブルからのデータ間に 1 対多の関係がある場合に JSON の結果がどのように表示されるかが含まれています。

返された JSON に null 値が存在しないことも示されています。 ただし、この既定の動作は、`FOR` 句で `INCLUDE_NULL_VALUES` キーワードを使用することでオーバーライドできます。

```sql
go

DROP TABLE IF EXISTS #tabStudent;
DROP TABLE IF EXISTS #tabClass;

go

CREATE TABLE #tabClass
(
   ClassGuid   uniqueIdentifier  not null  default newid(),
   ClassName   nvarchar(32)      not null
);

CREATE TABLE #tabStudent
(
   StudentGuid   uniqueIdentifier  not null  default newid(),
   StudentName   nvarchar(32)      not null,
   ClassGuid     uniqueIdentifier      null   -- Foreign key.
);

go

INSERT INTO #tabClass
      (ClassGuid, ClassName)
   VALUES
      ('DE807673-ECFC-4850-930D-A86F921DE438', 'Algebra Math'),
      ('C55C6819-E744-4797-AC56-FF8A729A7F5C', 'Calculus Math'),
      ('98509D36-A2C8-4A65-A310-E744F5621C83', 'Art Painting')
;

INSERT INTO #tabStudent
      (StudentName, ClassGuid)
   VALUES
      ('Alice Apple', 'DE807673-ECFC-4850-930D-A86F921DE438'),
      ('Alice Apple', 'C55C6819-E744-4797-AC56-FF8A729A7F5C'),
      ('Betty Boot' , 'C55C6819-E744-4797-AC56-FF8A729A7F5C'),
      ('Betty Boot' , '98509D36-A2C8-4A65-A310-E744F5621C83'),
      ('Carla Cap'  , null)
;

go

SELECT
      c.ClassName,
      s.StudentName
   from
                       #tabClass   as c
      RIGHT OUTER JOIN #tabStudent as s ON s.ClassGuid = c.ClassGuid
   --where
   --   c.ClassName LIKE '%Math%'
   order by
      c.ClassName,
      s.StudentName
   FOR
      JSON AUTO
      --, INCLUDE_NULL_VALUES
;

go

DROP TABLE IF EXISTS #tabStudent;
DROP TABLE IF EXISTS #tabClass;

go
```

次に示すのは、上記の SELECT により出力される JSON です。

```json
JSON_F52E2B61-18A1-11d1-B105-00805F49916B

[
   {"s":[{"StudentName":"Carla Cap"}]},
   {"ClassName":"Algebra Math","s":[{"StudentName":"Alice Apple"}]},
   {"ClassName":"Art Painting","s":[{"StudentName":"Betty Boot"}]},
   {"ClassName":"Calculus Math","s":[{"StudentName":"Alice Apple"},{"StudentName":"Betty Boot"}]}
]
```

### <a name="more-info-about-for-json-auto"></a>FOR JSON AUTO に関する詳細情報

詳細と例については、「[AUTO モードで自動的に JSON 出力を書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)」を参照してください。

構文と使用法については、「 [FOR 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="control-other-json-output-options"></a>他の JSON 出力オプションを制御する  
**FOR JSON** 句の出力を制御するには、次の追加オプションを使用します。  
  
-   **ROOT**。 JSON 出力に最上位の単一要素を追加するには、 **ROOT** オプションを指定します。 このオプションを指定しないと、JSON 出力にはルート要素がありません。 詳細については、「 [ROOT オプションを使用して JSON 出力にルート ノードを追加する &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)。  
  
-   **INCLUDE_NULL_VALUES**。 JSON 出力に null 値を含めるには、 **INCLUDE_NULL_VALUES** オプションを指定します。 このオプションを指定しないと、出力にはクエリ結果の NULL 値に対する JSON プロパティは含まれません。 詳細については、[INCLUDE_NULL_VALUES オプションを使用して JSON の出力に Null 値を含める &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md) に関する記事をご覧ください。   

-   **WITHOUT_ARRAY_WRAPPER**。 既定で **FOR JSON** 句の JSON 出力を囲んでいる角かっこを削除するには、 **WITHOUT_ARRAY_WRAPPER** オプションを指定します。 このオプションを使用して、1 行の結果からの出力として単一の JSON オブジェクトを生成します。 このオプションを指定しないと、JSON 出力は配列として書式設定されます。つまり、角かっこで囲まれます。 詳細については、「 [WITHOUT_ARRAY_WRAPPER オプションを使用して JSON 出力から角かっこを削除する &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 句の出力  
**FOR JSON** 句の出力には、次の特徴があります。  
  
1.  結果セットには 1 つの列が含まれます。
    -   小さな結果セットには 1 つの行が含まれます。
    -   大きな結果セットでは、長い JSON 文字列が複数行に分割されます。
        -   出力設定が**結果をグリッドに表示**の場合、SQL Server Management Studio (SSMS) は既定で結果を単一行に連結します。 SSMS のステータス バーに、実際の行数が表示されます。
        -   他のクライアント アプリケーションでは、複数の行の内容を連結することによって長い結果を単一の有効な JSON 文字列に結合し直すにはコードが必要になることがあります。 C# アプリケーションでのこのコードの例については、「[C# クライアント アプリで FOR JSON 出力を使用する](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md#use-for-json-output-in-a-c-client-app)」をご覧ください。
  
     ![FOR JSON 出力の例](../../relational-databases/json/media/forjson-example2.png)  
  
2.  結果は JSON オブジェクトの配列として書式設定されます。  
  
    -   JSON 配列の要素の数は、(FOR JSON 句が適用される前の) SELECT ステートメントの結果の行数と同じです。 
  
    -   (FOR JSON 句が適用される前の) SELECT ステートメントの結果の各行は、配列内の個別の JSON オブジェクトになります。  
  
    -   (FOR JSON 句が適用される前の) SELECT ステートメントの結果の各列は、JSON オブジェクトのプロパティになります。  
  
3.  列の名前とその値は、JSON の構文に従ってエスケープされます。 詳細については、「 [FOR JSON での特殊文字のエスケープと制御文字 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)。

### <a name="example"></a>例
**FOR JSON** 句による JSON 出力の書式設定の例を次に示します。  
  
**クエリ結果**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|×|  
|20|21|22|Y|  
|30|31|32|Z|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
 **JSON 出力**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  

 **FOR JSON** 句の出力に表示される内容の詳細については、次のトピックを参照してください。  

-   [FOR JSON が SQL Server データ型を JSON データ型に変換する方法 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
    **FOR JSON** 句では、このトピックで説明する規則を使用して、JSON 出力で SQL データ型を JSON 型に変換します。  

-   [FOR JSON での特殊文字のエスケープと制御文字 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
    **FOR JSON** 句は、このトピックで説明する形式で JSON 出力の特殊文字をエスケープし、制御文字を表します。  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [FOR 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [SQL Server およびクライアント アプリでの FOR JSON 出力の使用 &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  
