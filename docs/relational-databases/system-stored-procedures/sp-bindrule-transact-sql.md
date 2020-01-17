---
title: sp_bindrule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76d1572e1f99162c8daebeafadb0c8d75a53a4d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046027"
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  列またはエイリアス データ型にルールをバインドします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[Unique 制約と Check 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md)代わりにします。 チェックのキーワードを使用して制約を作成するかを確認、[テーブルの作成](../../t-sql/statements/create-table-transact-sql.md)または[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)ステートメントです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @rulename = ] 'rule'` CREATE RULE ステートメントで作成されたルールの名前です。 *ルール*、 **nvarchar(776)** の既定値はありません。  
  
`[ @objname = ] 'object_name'` テーブルと列、または別名データ型は、ルールのバインド先となります。 **text**、**ntext**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、CLR ユーザー定義型、**timestamp** の列には、ルールをバインドできません。 ルールは、計算列にバインドできません。  
  
 *object_name*は**nvarchar (776)** 既定値はありません。 場合*object_name*は 1 つの要素名では、別名データ型として解決されます。 テーブルおよび列として解決が最初に 2 または 3 つの要素名の場合は、この解決が失敗した場合、エイリアス データ型として解決します。 既存の別名データ型の列を継承する既定では、*ルール*ルールを直接その列にバインドしない限り、します。  
  
> [!NOTE]  
>  *object_name* 、角かっこを含めることができます **[** と **]** 文字で区切られた識別子の文字として。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
> [!NOTE]  
>  別名データ型を使用する式に対して作成されたルールは、列または別名データ型にバインドできますが、参照されてもコンパイルできません。 別名データ型に対して作成されたルールは使用しないでください。  
  
`[ @futureonly = ] 'futureonly_flag'` エイリアス データ型にルールをバインドする場合にのみ使用されます。 *future_only_flag*は**varchar (15)** 既定値は NULL です。 このパラメーターを設定すると**futureonly**エイリアス データ型の既存の列を新しいルールを継承しないようにします。 場合*futureonly_flag*が null の場合、新しいルールを現在ルールがあるいないか、別名データ型の既存のルールを使用している別名データ型の列にバインドされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 (ただし、CHECK 制約を使用することを推奨)、新しいルールを列にバインドすることができます、別名データ型にする、または**sp_bindrule**せず、既存のルールをバインド解除します。 元のルールはオーバーライドされます。 既に CHECK 制約のある列にルールをバインドすると、すべての制限が評価されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型にはルールをバインドできません。  
  
 INSERT ステートメントを試行すると、バインディングではなく、ルールが適用されます。 列に文字のルールをバインドすることができます**数値**このような INSERT 操作は有効ではありませんが、データを入力します。  
  
 別名データ型の既存の列がない限り、新しい規則を継承*futureonly_flag*として指定されて**futureonly**します。 常にエイリアス データ型で定義された新しい列は、ルールを継承します。 しかし、ALTER TABLE ステートメントの ALTER COLUMN 句によって、列のデータ型をルールがバインドされた別名データ型に変更すると、データ型にバインドしているルールはその列に継承されません。 ルールする必要があります具体的には列にバインドするを使用して**sp_bindrule**します。  
  
 関連情報を追加する列にルールをバインドすると、 **sys.columns**テーブルです。 関連情報を追加するエイリアス データ型にルールをバインドすると、 **sys.types**テーブルです。  
  
## <a name="permissions"></a>アクセス許可  
 テーブル列にルールをバインドするには、そのテーブルに対する ALTER 権限が必要です。 エイリアス データ型にアクセス許可を制御したりするタイプが属している、エイリアス データ型にルールをバインドするために必要なスキーマを変更する許可。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. ルールを列にバインドします。  
 というルール`today`が作成された次の例がするルールをバインドするルールを作成するステートメントを使用して現在のデータベースで、`HireDate`の列、`Employee`テーブルです。 行が `Employee` テーブルに追加されると、`HireDate` 列のデータは `today` ルールと照らし合わせてチェックされます。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. 別名データ型にルールをバインドする  
 `rule_ssn` という名前のルールがあり、`ssn` という名前の別名データ型があるものとします。次の例では、`rule_ssn` を `ssn` にバインドします。 CREATE TABLE ステートメントで、型の列で`ssn`を継承、`rule_ssn`ルールです。 型の既存の列`ssn`も継承、`rule_ssn`ルールは、しない限り、 **futureonly**が指定されて*futureonly_flag*、または`ssn`に直接バインドされたルールがあります。 常に列にバインドされたルールは、データ型にバインドされているものよりも優先されます。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Futureonly_flag を使用します。  
 次の例では、`rule_ssn` ルールを別名データ型 `ssn` にバインドします。 `futureonly` が指定されているため、`ssn` 型の既存の列は影響を受けません。  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子を使用します。  
 次の例で区切られた識別子の使用を示しています。 *object_name*パラメーター。  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
