---
title: sp_bindefault (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 918f545dd0ea0ca30524a307f1ae6d30c3fafb61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046048"
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  デフォルトを列または別名データ型にバインドします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 既定のキーワードを使用して既定の定義を作成することをお勧め、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)または[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)ステートメント代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @defname = ] 'default'` CREATE DEFAULT で作成される既定の名前です。 *既定*は**nvarchar (776)** 、既定値はありません。  
  
`[ @objname = ] 'object_name'` テーブルと列、または既定値がバインドされる別名データ型の名前です。 *object_name*は**nvarchar (776)** 既定値はありません。 *object_name*を定義することはできません、 **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、 **xml**、または CLRユーザー定義の型。  
  
 場合*object_name*は 1 つの要素名では、別名データ型として解決されます。 テーブルおよび列として解決はまず 2 または 3 つの部分名の場合、この解決が失敗した場合、別名データ型として解決されます。 既定では、既存の別名データ型の列を継承*既定*既定値を直接その列にバインドしない限り、します。 既定値をバインドできません、**テキスト**、 **ntext**、**イメージ**、 **varchar (max)** 、 **nvarchar (max)** 、**varbinary (max)** 、 **xml**、**タイムスタンプ**、または CLR ユーザー定義型の列、IDENTITY プロパティを持つ列、計算列、または列を既定の制約を既に持っています。  
  
> [!NOTE]  
>  *object_name*角かっこを含めることができます **:operator[]** 区切られた識別子として。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
`[ @futureonly = ] 'futureonly_flag'` デフォルトを別名データ型をバインドするときにのみ使用されます。 *futureonly_flag*は**varchar (15)** 既定値は NULL です。 このパラメーターに設定すると**futureonly**、そのデータ型の既存の列は、新しいデフォルトを継承できません。 このパラメーターは、既定値を列にバインドする場合に使用されません。 場合*futureonly_flag*が null の場合、新しいデフォルトは現在既定値があるいないか、別名データ型の既存の既定値を使用している別名データ型の列にバインドします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 使用することができます**sp_bindefault**デフォルトをバインドする新しい列に、優先が既定の制約を使用して、または別名データ型を既存のデフォルトをアンバインドせずにします。 古い既定値はオーバーライドされます。 デフォルトをバインドすることはできません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]システム データ型または CLR ユーザー定義型です。 既定値はするがバインドされている、列と互換性がない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]バインドするときではなく、既定値を挿入するときにエラー メッセージを返します。  
  
 か、既定値は自身に直接バインドしない限り、別名データ型の既存の列が、新しいデフォルトを継承または*futureonly_flag*として指定されて**futureonly**します。 別名データ型の新しい列は、常にデフォルトを継承します。  
  
 関連する情報を追加の列にデフォルトをバインドするときに、 **sys.columns**カタログ ビューです。 関連情報を追加、別名データ型にデフォルトをバインドするときに、 **sys.types**カタログ ビューです。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーが、テーブルを所有またはのメンバーである必要があります、 **sysadmin**固定サーバー ロール、または**db_owner**と**db_ddladmin**固定データベース ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 既定値を列にバインドします。  
 既定の名前付き`today`によって、既定では、次の例のバインドの作成に既定の設定を使用して、現在のデータベースで定義されている、`HireDate`の列、`Employee`テーブル。 `Employee` テーブルに行を追加するときに、`HireDate` 列の入力がなければ、この列にデフォルト `today` が入力されます。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. デフォルトを別名データ型にバインドします。  
 `def_ssn` という名前のデフォルトと、`ssn` という別名データ型が既に存在しています。 次の例は、既定値を連結`def_ssn`に`ssn`します。 既定値が、別名データ型が割り当てられているすべての列によって継承されるテーブルが作成されると、`ssn`します。 既存の型の列**ssn**もデフォルトを継承**def_ssn**がない限り、 **futureonly**が指定されて*futureonly_flag*値または、列にデフォルトが直接バインドします。 列にバインドされているデフォルトは、データ型にバインドされているデフォルトより常に優先します。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Futureonly_flag を使用します。  
 次の例は、既定値を連結`def_ssn`別名データ型に`ssn`します。 **Futureonly**が指定されている型の既存の列`ssn`影響を受けます。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子を使用します。  
 次の例は、区切られた識別子を使用して`[t.1]`の*object_name*します。  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
