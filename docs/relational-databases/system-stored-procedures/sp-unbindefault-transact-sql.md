---
title: sp_unbindefault (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7616401e8dcc9461d5eb3c7d67aedccf3a8c7af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095880"
---
# <a name="spunbindefault-transact-sql"></a>sp_unbindefault (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースの列または別名データ型から、デフォルトをバインド解除 (削除) します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] DEFAULT キーワードを使用して、既定の定義を作成することをお勧め、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)または[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)ステートメント代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object_name'` テーブルと列、または元の既定値はバインドを解除するのには、別名データ型の名前です。 *object_name*は**nvarchar (776)** 、既定値はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、最初に列名に対して、次に別名データ型に対して、2 つの要素で構成される識別子の解決が試行されます。  
  
 別名データ型からデフォルトをバインド解除すると同じ既定値であるようなデータ型の列もバインドされています。 ただし、同じデータ型でも、デフォルトが直接バインドされている列は影響を受けません。  
  
> [!NOTE]  
>  *object_name*角かっこを含めることができます **:operator[]** として識別子の区切り文字。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
`[ @futureonly = ] 'futureonly_flag'` 別名データ型からデフォルトをアンバインドするときにのみ使用されます。 *futureonly_flag*は**varchar (15)** 、既定値は NULL です。 ときに*futureonly_flag*は**futureonly**、既存のデータ型の列には、指定された既定は失われません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 既定のテキストを表示するには、実行**sp_helptext**パラメーターとして既定の名前に置き換えます。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルからデフォルトをアンバインドするのには、列には、テーブルに対する ALTER 権限が必要です。 別名データからデフォルトをアンバインドするのには、型は、型に対する CONTROL 権限または型が属するスキーマに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-unbinding-a-default-from-a-column"></a>A. 列からデフォルトをバインド解除  
 次の例では、`hiredate` テーブルの `employees` 列からデフォルトをバインド解除します。  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>B. 別名データ型からデフォルトをバインド解除する  
 次の例では、別名データ型の `ssn` からデフォルトをバインド解除します。 既存および将来の型の列がバインド解除します。  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Futureonly_flag を使用します。  
 次の例では、別名データ型の将来の使用をバインド解除`ssn`既存の影響を与えずに`ssn`列。  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子を使用します。  
 次の例で区切られた識別子を使用して*object_name*パラメーター。  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
