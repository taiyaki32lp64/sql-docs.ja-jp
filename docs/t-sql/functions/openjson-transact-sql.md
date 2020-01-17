---
title: OPENJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 48cd04467283683cf1dc54f300b2c4ff21fb8248
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632141"
---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

**OPENJSON** は、JSON テキストを解析し、JSON 入力からのオブジェクトとプロパティを行と列として返すテーブル値関数です。 つまり、**OPENJSON** は、JSON ドキュメントに対する行セット ビューを提供します。 行セット内の列と、それらの列に入力するために使用する JSON プロパティのパスを明示的に指定できます。 **OPENJSON** は一連の行を返すため、他のテーブル、ビュー、またはテーブル値関数で使用するのと同じように、**OPENJSON** を [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの `FROM` 句で使用できます。  
  
**OPENJSON** を使用して JSON データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にインポートするか、JSON を直接使用できないアプリまたはサービスのために JSON データをリレーショナル形式に変換できます。  
  
> [!NOTE]  
>  **OPENJSON** 関数は、互換性レベル 130 以上でのみ使用できます。 データベースの互換性レベルが 130 よりも低い場合、SQL Server は **OPENJSON** 関数を見つけて実行することができません。 他の JSON 関数は、すべての互換性レベルで使用できます。
> 
> `sys.databases` ビューまたはデータベース プロパティで互換性レベルを確認できます。 次のコマンドを使用して、データベースの互換性レベルを変更できます。  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>
> 新しい Azure SQL データベースであっても、互換性レベル 120 が既定値の場合があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン")[Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

**OPENJSON** テーブル値関数は、最初の引数として指定された *jsonExpression* を解析し、式内の JSON オブジェクトからのデータを含む 1 つまたは複数の行を返します。 *jsonExpression* には、入れ子になったサブオブジェクトを含めることができます。 *jsonExpression* 内からサブオブジェクトを解析する場合は、JSON サブオブジェクトの **path** パラメーターを指定できます。

### <a name="openjson"></a>openjson

![OPENJSON TVF の構文](../../relational-databases/json/media/openjson-syntax.png "OPENJSON 構文")  

既定では、**OPENJSON** テーブル値関数は、*jsonExpression* で見つかった各 {key:value} ペアのキー名、値、および型を含む 3 つの列を返します。 別の方法として、*with_clause* を指定することで、**OPENJSON** が返す結果セットのスキーマを明示的に指定できます。
  
### <a name="with_clause"></a>with_clause
  
![OPENJSON TVF 内の WITH 句の構文](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON WITH 構文")

*with_clause* には、**OPENJSON** が返す列とそれらの型の一覧が含まれます。 既定では、**OPENJSON** は、*with_clause* に指定された列名を持つ *jsonExpression* 内のキーと照合されます ( (この場合のキーの一致は、大文字と小文字の区別があるという意味を含みます)。 列名がキー名と一致しない場合は、省略可能な *column_path* を指定できます。これは *jsonExpression* 内のキーを参照する [JSON パス式](../../relational-databases/json/json-path-expressions-sql-server.md) です。 

## <a name="arguments"></a>引数

### <a name="jsonexpression"></a>*jsonExpression*

JSON テキストを含む Unicode 文字式です。  
  
OPENJSON では、配列の要素または JSON 式内のオブジェクトのプロパティを反復処理し、各要素またはプロパティの 1 つの行を返します。 次の例では、*jsonExpression* として指定されたオブジェクトの各プロパティを返します。  

```sql
DECLARE @json NVarChar(2048) = N'{
   "String_value": "John",
   "DoublePrecisionFloatingPoint_value": 45,
   "DoublePrecisionFloatingPoint_value": 2.3456,
   "BooleanTrue_value": true,
   "BooleanFalse_value": false,
   "Null_value": null,
   "Array_value": ["a","r","r","a","y"],
   "Object_value": {"obj":"ect"}
}';

SELECT * FROM OpenJson(@json);
```

**結果:**

| キー (key)                                | value                 | 型 |
| :--                                | :----                 | :--- |
| String_value                       | John                  | 1 |
| DoublePrecisionFloatingPoint_value | 45                    | 2 |
| DoublePrecisionFloatingPoint_value | 2.3456                | 2 |
| BooleanTrue_value                  | true                  | 3 |
| BooleanFalse_value                 | false                 | 3 |
| Null_value                         | NULL                  | 0 |
| Array_value                        | ["a","r","r","a","y"] | 4 |
| Object_value                       | {"obj":"ect"}         | 5 |
| &nbsp; | &nbsp; | &nbsp; |

- DoublePrecisionFloatingPoint_value は、IEEE 754 に準拠します。

### <a name="path"></a>*path*

*jsonExpression* 内のオブジェクトまたは配列を参照する省略可能な JSON パス式です。 **OPENJSON** は、指定された位置で JSON テキストをシークし、参照先のフラグメントのみを解析します。 詳細については、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] と [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] では、*path* の値として変数を指定できます。
  
次の例では、*path* を指定することで、入れ子になったオブジェクトを返します。  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **結果**  
  
|Key|[値]|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  

**OPENJSON** が JSON 配列を解析するとき、この関数は、JSON テキスト内の要素のインデックスをキーとして返します。

JSON の式のプロパティを持つパスの手順を照合に使用する比較では、大文字と小文字および照合順序に関係なく (つまり、BIN2 の比較)。 

### <a name="with_clause"></a>*with_clause*

**OPENJSON** 関数が返す出力スキーマを明示的に定義します。 省略可能な *with_clause* には、次の要素を含めることができます。

*colName*。出力列の名前。  
  
**OPENJSON** は既定では、列の名前を使用して、JSON テキストのプロパティと一致します。 たとえば、*name*の列をスキーマを指定する場合、OPENJSON は JSON テキストには、"name"プロパティを使用して、この列を作成しようとします。 使用して、この既定のマッピングをオーバーライドすることができます、  *column_path* 引数。  
  
*type*  
出力列のデータ型。  

> [!NOTE]
> **AS JSON** オプションも使用する場合は、列の *type* を `NVARCHAR(MAX)` にする必要があります。
  
*column_path*  
指定した列で返されるプロパティを指定する JSON のパス。 詳細については、の説明を参照してください、*path* このトピックの前のパラメーター。  
  
出力列の名前がプロパティの名前の一致しない場合に既定のマッピング ルールをオーバーライドするには、*column_path* を使用します。  
  
パス ステップを JSON 式のプロパティと照合するために使われる比較では、大文字と小文字を区別し、照合順序に対応していません (つまり、BIN2 比較です)。  
  
パスの詳細については、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。  
  
*AS JSON*  
参照先のプロパティに内部 JSON オブジェクトまたは配列が含まれていることを指定するには、列定義の中で **AS JSON** を使用します。 **AS JSON** を指定する場合、列の型は NVARCHAR(MAX) にする必要があります。

- として **AS JSON** を指定しないと、列の場合、関数は、指定されたパスに指定された JSON プロパティからスカラー値 (たとえば、int、文字列、true、false) を返します。 パスがオブジェクトまたは配列を表しているときに、指定されたパスにプロパティが見つからない場合、関数は、lax モードでは null を、strict モードではエラーを返します。 この動作は、**JSON_VALUE** 関数の動作に似ています。  
  
- **AS JSON** の列を指定する場合、関数は、指定したパス指定された JSON プロパティからは JSON フラグメントを返します。 パスがスカラー値を表しているときに、指定されたパスにプロパティが見つからない場合、関数は、lax モードでは null を、strict モードではエラーを返します。 この動作は、**JSON_QUERY** 関数の動作に似ています。  
  
> [!NOTE]  
> JSON プロパティから入れ子になった JSON フラグメントを返す場合は、**AS JSON** フラグを指定する必要があります。 このオプションの指定がないときに、プロパティが見つからない場合、OPENJSON は、参照先の JSON オブジェクトまたは配列の代わりに NULL 値を返します。  
  
たとえば、次のクエリを返し、配列の要素の書式を設定します。  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
  {  
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]'  
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**結果**
  
|数値|date|Customer|Quantity|Order|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-により、|AW29825|1|{"Number":"SO43659","Date":"2011-05-31T00:00:00"}|  
|として SO43661|2011-06-01T00:00:00|AW73565|3|{"Number":"SO43661","Date":"2011-06-01T00:00:00"}|  
  
## <a name="return-value"></a>戻り値
OPENJSON 関数によって返される列は、WITH オプションによって異なります。  
  
1. OPENJSON を既定のスキーマで呼び出した場合 (つまり、WITH 句に明示的にスキーマを指定しない場合)、関数は、次の列を持つテーブルを返します。  
    1.  **[キー]** 指定したプロパティの名前か、指定した配列内の要素のインデックスを含む nvarchar (4000) 値。 キー列は BIN2 照合順序を持っています。  
    2.  **値**。 プロパティの値を含む、nvarchar (max) 値です。 [値] 列では、その照合順序を継承 *jsonExpression* から。
    3.  **型**。 値の型を含む int 値。 **型**の列には、既定のスキーマを OPENJSON を使用する場合にのみが返されます。 型の列では、次の values. のことがあります。  
  
        |型の列の値|JSON データ型|  
        |------------------------------|--------------------|  
        |0|null|  
        |1|string|  
        |2|int|  
        |3|true/false|  
        |4|array|  
        |5|object|  
  
     最初のレベル プロパティのみが返されます。 JSON のテキストが正しくフォーマットされていない場合、ステートメントが失敗します。  

2. -OPENJSON を呼び出すし、WITH 句で、明示的なスキーマを指定する、するときに、WITH 句で定義したスキーマを持つテーブルを返します。

> [!NOTE]  
> **Key**、**Value**、および **Type** 列が返されるのは、既定のスキーマで OPENJSON を使った場合のみです。明示的なスキーマでは使用できません。

## <a name="remarks"></a>Remarks  

**OPENJSON** の 2 番目の引数または *with_clause* で使用される *json_path* は、**lax** または **strict** キーワードで始めることができます。

- **lax** モードでは、指定のパスにオブジェクトまたは値が見つからない場合でも、**OPENJSON** はエラーを生成しません。 パスが見つからない場合、**OPENJSON** は、空の結果セットまたは NULL 値を返します。
- **Strict** モード では、パスが見つからない場合、**OPENJSON** はエラーを返します。

このページに示すいくつかの例では、パス モード (lax または strict) を明示的に指定しています。 パス モードの指定は必須ではありません。 パス モードを明示的に指定しない場合は、lax が既定のモードになります。 パス モードとパス式の詳細については、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。    

*with_clause* の列名は、JSON テキスト内のキーと照合されます。 列名 `[Address.Country]` を指定した場合は、`Address.Country` キーと照合されます。 オブジェクト `Address` 内の入れ子になったキー `Country` を参照する場合は、パス `$.Address.Country` を列のパスに指定する必要があります。

*json_path* には、英数字を使用したキーを含めることがあります。 キーに特殊文字がある場合は、二重引用符を使用して、*json_path* 内でキー名をエスケープします。 たとえば、`$."my key $1".regularKey."key with . dot"` は、次の JSON テキストの値 1 と一致します。

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>使用例  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>例 2 - JSON 配列を一時テーブルに変換します。

次の例では、識別子の一覧を数値の JSON 配列として指定します。 このクエリは、JSON 配列を識別子のテーブルに変換し、すべての製品を指定の ID でフィルター処理します。  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
このクエリは、次の例と同等です。 ただし、次の例では、数値をパラメーターとして渡す代わりに、クエリに埋め込む必要があります。  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>例 3 - 2 つの JSON オブジェクトからのマージ プロパティ

次の例では、2 つの JSON オブジェクトのすべてのプロパティの和集合を選択します。 2 つのオブジェクトでは、重複する*name*プロパティがあります。 例では、キーの値を使って、結果から重複する行を除外しています。  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>例 3 - CROSS APPLY を使用してテーブルのセルに格納されている JSON データを行と結合する

次の例では、`SalesOrderHeader` テーブルには、`SalesOrderReasons` の配列を JSON 形式で含んでいる`SalesReason` テキスト列があります。 `SalesOrderReasons` オブジェクトには、*Quality* や *Manufacturer* などのプロパティが含まれます。 例では、すべての販売注文の行を、関連する販売理由と結合するレポートを作成しています。 OPENJSON 演算子では、理由が別の子テーブルに格納されていたかのように、販売理由の JSON 配列を展開します。 次に、CROSS APPLY 演算子では、OPENJSON テーブル値関数によって返される行に各販売注文の行を結合します。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> 通常使用順に展開するときに、JSON 配列は、個々 のフィールドに格納されているし、その親の行との結合に、 [!INCLUDE[tsql](../../includes/tsql-md.md)] CROSS APPLY 演算子。 CROSS APPLY について詳しくは、[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) に関する記事をご覧ください。  
  
返される行の明示的に定義されたスキーマを指定した `OPENJSON` を使用することで、同じクエリを書き直すことができます。  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
この例では、`$` パスは、配列内の各要素を参照します。 返される値を明示的にキャストする場合は、この種類のクエリを使用できます。  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>例 4 - CROSS APPLY とリレーショナル行と JSON の要素を結合する

次のクエリは、次の表に示すように、リレーショナル行と JSON 要素を結果内で結合します。  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**結果**
  
|title|street|postcode|lon|lat|  
|-----------|------------|--------------|---------|---------|  
|Whole Food Markets|17991 Redmond Way|WA  98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA  98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>例 5 - インポートには、SQL Server の JSON データ

次の例では、全体の JSON オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルです。  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50))
```  
  
## <a name="see-also"></a>参照

 [JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [OPENJSON を使用して JSON データを行と列に変換する &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [既定のスキーマを使用する OPENJSON の使用&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [明示的なスキーマで OPENJSON を使用する&#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
