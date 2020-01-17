---
title: JSON_MODIFY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: d340d362301698f7dfaef28476ea659b948163bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109382"
---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  JSON 文字列内のプロパティの値を更新し、更新された JSON 文字列を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>引数

 *式 (expression)*  
 式。 通常、変数または JSON テキストを含む列の名前。  
  
 *式*に有効な JSON が含まれていない場合、**JSON_MODIFY** エラーが返されます。  
  
 *path*  
 更新するプロパティを指定する JSON path 式。

 *path* の構文は次のとおりです。  
  
 `[append] [ lax | strict ] $.<json path>`  
  
- *append*  
    *\<json path>* によって参照されるアレイに新しい値を追加する必要があることを指定する省略可能な修飾子。  
  
- *lax*  
    *\<json path>* によって参照されるプロパティは存在する必要がないことを指定します。 プロパティが存在しない場合、JSON_MODIFY は指定されたパスに新しい値を挿入しようとします。 パスにプロパティを挿入できない場合、挿入は失敗する可能性があります。 *lax* または *strict* の指定がない場合の既定のモードは *lax* です。  
  
- *strict*  
    *\<json path>* によって参照されるパスが JSON 式内に存在する必要があることを指定します。 プロパティが存在しない場合、JSON_MODIFY はエラーを返します。  
  
- *\<json path>*  
    更新するプロパティのパスを指定します。 詳細については、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。  
  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] と [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] では、*path* の値として変数を指定できます。

*path* の書式が有効でない場合、**JSON_MODIFY** はエラーを返します。  
  
 *newValue*  
 *path* によって指定されるプロパティの新しい値。  
  
 lax モードでは、新しい値が NULL の場合、JSON_MODIFY は指定されたキーを削除します。  
  
JSON_MODIFY は、値の型が NVARCHAR または VARCHAR の場合は、新しい値のすべての特殊文字をエスケープします。 テキスト値は、FOR JSON、JSON_QUERY、または JSON_MODIFY によって生成され、適切に書式設定された JSON の場合はエスケープされません。  
  
## <a name="return-value"></a>戻り値

 *expression* の更新された値を、適切に書式設定された JSON テキストとして返します。  
  
## <a name="remarks"></a>Remarks

 JSON_MODIFY 関数を使用して、既存のプロパティの値の更新、新しいキーと値のペアの挿入、またはモードと指定された組み合わせに基づくキーの削除を実行できます。  
  
 次の表は、lax モードと strict モードでの **JSON_MODIFY** の動作を比較します。 省略可能なパス モード (厳密でない、または厳格) の指定について詳しくは、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。  
  
|既存の値|パスが存在するか|厳密でないモード|厳格モード|  
|--------------------|-----------------|--------------|-----------------|  
|NULL 以外|はい|既存の値を更新します。|既存の値を更新します。|  
|NULL 以外|いいえ|指定したパスに新しいキーと値のペアを作成しようとします。<br /><br /> これは失敗する場合があります。 たとえば、パス `$.user.setting.theme` を指定したときに、`$.user` または `$.user.settings` オブジェクトが存在しないか、設定がアレイまたはスカラー値の場合、JSON_MODIFY はキー `theme` を挿入しません。|Error - INVALID_PROPERTY|  
|NULL|はい|既存のプロパティを削除します。|既存の値を null に設定します。|  
|NULL|いいえ|NO ACTION 最初の引数が結果として返されます。|Error - INVALID_PROPERTY|  
  
 lax モードでは、JSON_MODIFY は、新しいキーと値のペアを作成しようとしますが、その操作は、場合によっては失敗します。  
  
## <a name="examples"></a>使用例  
  
### <a name="example---basic-operations"></a>例 - 基本的な操作

 次の例では、JSON テキストを使用して実行できる基本的な操作を示します。  
  
 **クエリ**
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **結果**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>例 - 複数の更新

 JSON_MODIFY では、1 つのプロパティのみを更新できます。 複数の更新を実行する必要がある場合は、複数の JSON_MODIFY 呼び出しを使用できます。  
  
 **クエリ**
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **結果**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>例 - キーの名前変更  
 次の例では、JSON_MODIFY 関数を使用して、JSON テキスト内のプロパティの名前を変更する方法を示します。 最初に、既存のプロパティの値を取得し、それを新しいキーと値のペアとして挿入できます。 次に、古いプロパティの値を NULL に設定することで、古いキーを削除できます。  
  
 **クエリ**
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **結果**
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 新しい値が数値型にキャストされない場合、JSON_MODIFY は、それをテキストとして処理し、二重引用符で囲みます。  
  
### <a name="example---increment-a-value"></a>例 - 値の増分

 次の例では、JSON_MODIFY 関数を使用して、JSON テキスト内のプロパティの値を変更する方法を示します。 最初に、既存のプロパティの値を取得し、それを新しいキーと値のペアとして挿入できます。 次に、古いプロパティの値を NULL に設定することで、古いキーを削除できます。  
  
 **クエリ**
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **結果**
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>例 - JSON オブジェクトの変更

 JSON_MODIFY では、その中に適切に書式設定された JSON テキストが含まれている場合でも、*newValue* 引数をプレーン テキストとして処理します。 その結果、次の例に示すように、この関数の JSON の出力は二重引用符で囲まれ、すべての特殊文字がエスケープされます。  
  
 **クエリ**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **結果**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 自動エスケープを回避するには、JSON_QUERY 関数を使用して *newValue* を指定します。 JSON_MODIFY は、JSON_MODIFY によって返される値が適切に書式設定された JSON であることを認識するため、値をエスケープすることはありません。  
  
 **クエリ**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **結果**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>例 - JSON 列の更新

 次の例では、JSON を含むテーブル列のプロパティの値を更新します。  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>参照

 [JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON データ &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  