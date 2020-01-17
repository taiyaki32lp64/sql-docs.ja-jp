---
title: DBCC CHECKIDENT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 2a3c1885d6796977ea48585858fa5d2a271e6a46
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798374"
---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  指定された [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のテーブルの現在の ID 値をチェックし、必要に応じて ID 値を変更します。 ID 列の新しい現在の ID 値を手動で設定する場合に DBCC CHECKIDENT を使用することもできます。  
  
 ![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```console

-- Syntax for SQL Server and Azure SQL Database  

DBCC CHECKIDENT
 (
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  

```console
-- Syntax for Azure SQL Data Warehouse
DBCC CHECKIDENT   
 (   
    table_name  
        [RESEED, new_reseed_value ]   
)  
[ WITH NO_INFOMSGS ]  

```
## <a name="arguments"></a>引数

 *table_name*  
 現在の ID 値をチェックするテーブルの名前です。 指定されたテーブルには、ID 列が含まれている必要があります。 テーブル名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 'Person.AddressType' や [Person.AddressType] など、2 つまたは 3 つの部分名を区切る必要があります。
  
 NORESEED  
 現在の ID 値を変更しないように指定します。  
  
 RESEED  
 現在の ID 値を変更するように指定します。  
  
 *new_reseed_value*  
 ID 列の現在値として使用する新しい値を指定します。  
  
 WITH NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks

 現在の ID 値に加えられる特定の修正は、指定されているパラメーターによって異なります。  
  
|DBCC CHECKIDENT コマンド|ID の修正または加えられた修正|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *table_name*, NORESEED )|現在の ID 値はリセットされません。 DBCC CHECKIDENT は、ID 列の現在の ID 値と現在の最大値を返します。 2 つの値が異なる場合は、エラーが発生しないよう、または連続値の一部が欠落しないように、ID 値をリセットする必要があります。|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> 内の複数の<br /><br /> DBCC CHECKIDENT ( *table_name*, RESEED )|テーブルの現在の ID 値が、ID 列に格納されている最大の ID 値より小さい場合、テーブルの現在の ID 値は ID 列の最大値にリセットされます。 後の「例外」のセクションを参照してください。|  
|DBCC CHECKIDENT ( *table_name*, RESEED, *new_reseed_value* )|現在の ID 値は *new_reseed_value* に設定されます。 テーブルが作成された後、そのテーブルに行が挿入されていない、または TRUNCATE TABLE ステートメントを使用してすべての行が削除された場合、DBCC CHECKIDENT を実行した後に挿入された最初の行が ID として *new_reseed_value* を使用します。 テーブルに行が存在する場合、または DELETE ステートメントを使用してすべての行が削除された場合は、挿入される次の行に *new_reseed_value* + [現在の増分](../../t-sql/functions/ident-incr-transact-sql.md)の値が使用されます。 トランザクションによって行が挿入され、後でそのトランザクションがロールバックされた場合、挿入される次の行では、*new_reseed_value*  + [現在の増分](../../t-sql/functions/ident-incr-transact-sql.md)の値が、行が削除されたかのように使用されます。 テーブルが空でない場合、ID 値に ID 列の最大値より小さな値を設定すると、次の状況のいずれかが発生する可能性があります。<br /><br /> ID 列に PRIMARY KEY 制約または UNIQUE 制約が設定されている場合、生成される ID 値と既存の値との競合が原因で、テーブルに対する後続の挿入操作でエラー メッセージ 2627 が生成されます。<br /><br /> PRIMARY KEY 制約または UNIQUE 制約が設定されていない場合、後続の挿入操作では重複した ID 値が挿入されます。|  
  
## <a name="exceptions"></a>例外

 次の表に、DBCC CHECKIDENT で現在の ID 値が自動的にリセットされないときの条件と、ID 値をリセットする方法を示します。  
  
|条件|リセット方法|  
|---------------|-------------------|  
|現在の ID 値がテーブルの最大値より大きい。|DBCC CHECKIDENT (*table_name*, NORESEED) を実行して、列の現在の最大値を判断します。 次に、DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) コマンドで値を *new_reseed_value* に指定します。<br /><br /> -または-<br /><br /> *new_reseed_value* を非常に低い値に設定して DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) を実行してから DBCC CHECKIDENT (*table_name*, RESEED) を実行して値を修正します。|  
|すべての行がテーブルから削除されている。|*new_reseed_value* を新しい開始値に設定して DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) を実行します。|  
  
## <a name="changing-the-seed-value"></a>シード値の変更

 シード値は、テーブルに読み込まれる最初の行の ID 列に挿入される値です。 以降の行にはすべて、現在の ID 値 (テーブルまたはビューに対して生成された最後の ID 値) に増分値を加えた値が格納されます。  
  
 DBCC CHECKIDENT は、次のタスクには使用できません。  
  
- テーブルまたはビューの作成時に ID 列に指定された、元のシード値を変更する。  
  
- テーブルまたはビュー内の既存の行にシード値を再生成する。  
  
 元のシード値を変更したり、任意の既存の行にシード値を再生成したりするには、ID 列を削除し、新しいシード値を指定して作り直す必要があります。 テーブルにデータが含まれている場合、ID 番号が、指定のシード値および増分値を使用して既存の行に追加されます。 行の更新順序は保証されません。  
  
## <a name="result-sets"></a>結果セット

 ID 列を含むテーブルに対してオプションを指定するかどうかにかかわらず、DBCC CHECKIDENT は、ある操作以外のすべての操作に対して次のメッセージを返します。 それは、新しいシード値を指定する操作です。  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 RESEED *new_reseed_value* を使用して新しいシード値を指定する DBCC CHECKIDENT を使用する場合、次のメッセージが返されます。  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>アクセス許可

 呼び出し元がテーブルを含むスキーマを所有しているか、**sysadmin** 固定サーバー ロール、**db_owner** 固定サーバー ロール、または **db_ddladmin** 固定サーバー ロールのメンバーである必要があります。

Azure SQL Data Warehouse には **db_owner** アクセス許可が必要です。
  
## <a name="examples"></a>使用例  
  
### <a name="a-resetting-the-current-identity-value-if-its-needed"></a>A. 必要に応じて現在の ID 値をリセットする  
 次の例では、必要に応じて、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の指定されたテーブルの現在の ID 値をリセットします。  
  
```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. 現在の ID 値を報告する

 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の指定されたテーブルの現在の ID 値を報告します。ID 値が正しくない場合でも、ID 値の修正は行いません。  
  
```sql
USE AdventureWorks2012;
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);
GO  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. 現在の ID 値を強制的に新しい値に設定する  
 次の例では、 `AddressType` テーブルの `AddressTypeID` 列の現在の ID 値を強制的に 10 に設定します。 テーブルには既存の行があるため、挿入される次の行には値として 11 が使用されます。列に定義された新しい現在の ID 値に 1 (列の増分値) を加えた値です。  

```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
```

### <a name="d-resetting-the-identity-value-on-an-empty-table"></a>D. 空のテーブルの ID 値をリセットする

 次の例では、テーブルのすべてのレコードを削除した後に、`ErrorLog` テーブルの `ErrorLogID` 列の現在の ID 値を強制的に 1 に設定します。 テーブルには既存の行がないため、次に挿入される行では値に 1 が使用されます。この値は、列について定義された増分値を加えない現在の ID 値です。  
  
```sql
USE AdventureWorks2012;  
GO  
TRUNCATE TABLE dbo.ErrorLog
GO
DBCC CHECKIDENT ('dbo.ErrorLog', RESEED, 1);  
GO  
```  
  
## <a name="see-also"></a>参照

[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
