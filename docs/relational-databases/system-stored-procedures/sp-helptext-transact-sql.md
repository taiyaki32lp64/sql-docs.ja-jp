---
title: sp_helptext (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 160d52c8c145828f6a63c104aecb17e04867cee8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048289"
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ユーザー定義ルール、既定では、暗号化されていない状態の定義を表示します[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャ、ユーザー定義[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャの関数、トリガー、計算列、CHECK 制約、ビュー、またはシステムなどのシステム オブジェクトです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'name'` ユーザー定義のスキーマ スコープ オブジェクトの修飾付きまたは修飾なしの名前です。 引用符は、修飾されたオブジェクトが指定されている場合にのみ必要です。 データベース名を含む、完全修飾名が指定されている場合、データベース名は、現在のデータベースの名前である必要があります。 オブジェクトは、現在のデータベースでなければなりません。 *名前*は**nvarchar (776)** 、既定値はありません。  
  
`[ @columnname = ] 'computed_column_name'` 定義情報を表示する計算列の名前です。 列を含むテーブルとして指定する必要があります*名前*します。 *column_name*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Text**|**nvarchar (255)**|オブジェクトの定義|  
  
## <a name="remarks"></a>コメント  
 sp_helptext は、複数の行でオブジェクトを作成するために使用される定義を表示します。 行ごとに 255 文字が含まれています、[!INCLUDE[tsql](../../includes/tsql-md.md)]定義します。 定義が存在する、**定義**内の列、 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)カタログ ビューです。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 システム オブジェクトの定義は、公開されます。 ユーザー オブジェクトの定義は、オブジェクトの所有者、または次のいずれかの権限を許可された人が表示できます。ALTER、CONTROL、TAKE OWNERSHIP、VIEW DEFINITION。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. トリガーの定義を表示します。  
 次の例は、トリガーの定義を表示します。`dEmployee`で、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. 計算列の定義を表示する  
 次の例は、計算列の定義を表示します。`TotalDue`上、`SalesOrderHeader`テーブルに、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース。  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
